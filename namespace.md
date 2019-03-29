# Namespaces系统

Linux内核的Namespaces机制，被用来隔离不同的进程可以访问的系统资源。

## 进程的名字空间(Namespaces)

Linux系统中，每个进程都有所属的名字空间(Namespaces)，使用如下命令可以查看进程的名字空间(Namespaces)：

```
ls /proc/PID/ns

例如：
ls -l /proc/26885/ns
total 0
lrwxrwxrwx 1 root root 0 Mar 27 15:43 cgroup -> 'cgroup:[4026532610]'
lrwxrwxrwx 1 root root 0 Mar 27 15:43 ipc -> 'ipc:[4026532532]'
lrwxrwxrwx 1 root root 0 Mar 27 15:43 mnt -> 'mnt:[4026532530]'
lrwxrwxrwx 1 root root 0 Mar 27 15:43 net -> 'net:[4026532535]'
lrwxrwxrwx 1 root root 0 Mar 27 15:43 pid -> 'pid:[4026532533]'
lrwxrwxrwx 1 root root 0 Mar 27 15:43 pid_for_children -> 'pid:[4026532533]'
lrwxrwxrwx 1 root root 0 Mar 27 15:43 user -> 'user:[4026531837]'
lrwxrwxrwx 1 root root 0 Mar 27 15:43 uts -> 'uts:[4026532531]'
```

进程所属的每个Namespace，都在`/proc/PID/ns`目录下都有一个对应的符号连接文件。

> 每个Namespace里，到底有什么？怎么查看？

## 名字空间(Namespace)的内核实现

目前Linux内核提供7种Namesapce(cgroup, mnt, uts, ipc, pid, net, user)，分别针对7种系统资源。

| 名字空间      | 内核编译选项     | 相关标志         |  说明       |
|---------------|------------------|------------------|-------------|
| cgroup        | CONFIG_CGROUPS   | CLONE_NEWCGROUP  | 4.6 引入, 与cgroup v2关系密切  |
| mnt           | 缺省             | CLONE_NEWNS      | 2.4.19 引入，针对文件系统的挂载点                          |
| uts           | CONFIG_UTS_NS    | CLONE_NWUTS      | 2.6.19 引入，这对hostname和domainname两个系统标识          |
| ipc           | CONFIG_IPC_NS    | CLONE_NEWIPC     | 2.6.19 引入，针对IPC资源(SystemV IPC, Posix message Queue) |
| pid           | CONFIG_PID_NS    | CLONE_NEWPID     | 2.6.24 引入，针对系统中的PID Number  |
| net           | CONFIG_NET_NS    | CLONE_NEWNET     | 2.6.24 引入，针对系统中的网络资源，每个net namesapce都有自己的网络设备，IP地址，路由表，/proc/net/目录，端口号等   |
| user          | CONFIG_USER_NS   | CLONE_NEWUSER    | 2.6.23 引入，针对User 和 Group ID Number。从3.8 开始，非特权进程也能创建 User Namespace  |

Linux内核提供有三个与名字空间(Namespace)相关的系统调用：

* 在clone创建新进程时，通过特定的标识，控制新进程与父进程共享Namespace，还是创建新的Namespace。
* unshare系统调用会创建一个新的Namespace，并将当前进程放入该Namespace。
* setns系统调用将当前进程放入一个已经存在的Namesapce。

| 系统调用  | 接口  |
|-----------|-------|
| clone     | int clone(int (\*fn)(void \*), void \*, int, void \* );  |
| unshare   | int unshare(int flags);           |
| setns     | int setns(int fd, int nstype);    |

