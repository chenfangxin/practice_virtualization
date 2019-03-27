# Namespace系统

使用Namespace可以实现系统资源的隔离，目前Linux内核提供7种Namesapce(cgroup, mnt, uts, ipc, pid, net, user)，分别针对7种系统资源。

| 名字空间      | 内核选项              |  说明       |
|---------------|-----------------------|-------------|
| cgroup        | CONFIG_CGROUPS        |   |
| mnt           |                       | 2.4.19 引入，针对文件系统的挂载点                          |
| uts           | CONFIG_UTS_NS         | 2.6.19 引入，这对hostname和domainname两个系统标识          |
| ipc           | CONFIG_IPC_NS         | 2.6.19 引入，针对IPC资源(SystemV IPC, Posix message Queue) |
| pid           | CONFIG_PID_NS         | 2.6.24 引入，针对系统中的PID Number  |
| net           | CONFIG_NET_NS         | 2.6.24 引入，针对系统中的网络资源    |
| user          | CONFIG_USER_NS        | 2.6.23 引入，针对User 和 Group ID Number  |

