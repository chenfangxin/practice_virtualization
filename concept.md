# 虚拟化技术分类

通常所说的虚拟化(Virtualization)技术，是指“计算虚拟化”，即为软件系统提供相互隔离的运行环境。

要实现隔离，目前有两种模式 ：虚拟机 和 容器。

+ 虚拟机(Virtual Machine) ：能实现从操作系统到用户空间的完全隔离

+ 容器(Conatiner)：只实现用户空间运行环境的隔离

借用Docker的一张图来说明：

![虚拟机与容器对比](./imgs/vm_container.png)

--------------------
#### 虚拟机

目前，以虚拟机方式实现的虚拟化环境有：

+ VMware
+ [XEN](XEN.md)
+ [QEMU/KVM](KVM.md)

要虚拟机跑起来，关键是要解决[`临界指令`](x86_problem.md)问题，有三种方法解决这个问题：

+ 全虚拟化(Full-Virtualization)：使用BT(Binary Transition)技术，替换Guest OS中的不能虚拟化的指令。VMware支持这种方式

+ 半虚拟化(Para-Virtualization)：修改Guest OS代码，替换掉可能出错的部分。早期的XEN使用这种方式

+ 硬件辅助虚拟化(Hardware-assisted Virtualization)：利用CPU对虚拟化提供的特殊支持，比如Intel VT-x或AMD-v技术，目前几乎所有的厂家都支持这种方式。

要深入理解硬件辅助虚拟化，详见[HVM](HVM.md)。

[Jailhouse](Jailhouse.md)是另一类基于硬件辅助的虚拟化技术。

--------------------
#### 容器

目前，以容器方式实现的虚拟化环境有： 

+ [LXC](lxc.md)
+ [Docker](docker.md)

Linux的`容器`主要是基于[namespace](namespace.md)和[Cgroup](cgroup.md)两个子系统实现的。利用这两个子系统，实现用户空间运行环境的隔离，但是内核还是共用的。

现在还有将虚拟机和容器相结合的技术方案，比如FaceBook推出的[kata container](kata_container.md)，还有Amazon AWS推出的[firecracker](firecracker.md)。

--------------------
#### 沙箱(SandBox)

+ gVisor

