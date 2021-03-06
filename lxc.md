# LXC

## 使用LXC

主机平台使用CentOS7，lxc-1.0支持到2019年，lxc-2.0支持到2021年。

#### 编译，安装LXC

```
wget -c https://linuxcontainers.org/downloads/lxc/lxc-3.0.1.tar.gz
tar xf lxc-3.0.1.tar.gz
cd lxc-3.0.1
./autogen.sh
./configure
make
make install

systemctl enable --now lxc
systemctl status lxc

lxc-checkconfig
```

#### 创建LXC容器

1. 下载LXC Rootfs

```
wget -c https://mirrors.tuna.tsinghua.edu.cn/lxc-images/images/centos/7/amd64/default/20180806_02:16/rootfs.tar.xz

tar xf rootfs.tar.xz
```

#### LXC的原理

LXC主要基于如下内核特性：

* [Kernel Namespace](namespace.md)
* [CGroups](cgroup.md)

LXC还使用如下安全特性：
* [Chroots (using pivort_root)](chroot.md)
* [Apparmor and SELinux profiles](apparmor_and_selinux.md)
* [Seccomp policies](seccomp.md)
* [Kernel Capabilities](capabilities.md)

> 引申阅读 [Linux Security Module](lsm.md)

----------------------------------------

## 使用LXD

lxd是下一代容器管理工具，并不是重写了lxc，而是基于lxc，并提供比lxc更友好的使用体验。lxd是一个守护进程(daemon)，提供RESTful API。lxd用go语言实现，lxd-3.0支持到2023年。

#### 安装LXD

使用 ganto/lxc3 repo，用如下命令安装lxc和lxd：

```
wget -c https://copr.fedorainfracloud.org/coprs/ganto/lxc3/repo/epel-7/ganto-lxc3-epel-7.repo

yum install lxc lxc-templates
yum install lxd lxd-client lxd-tools
```

#### 使用LXD  

```
yum install libvirt
systemctl enable --now libvirt

systemctl enable --now lxc

usermod -a -G lxd root
echo "root:1000000:65536" >> /etc/subuid
echo "root:1000000:65536" >> /etc/subgid

systemctl enable --now lxd

source /etc/profile
lxd init

lxc list
lxc image list
```


