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

systemctl start lxc
systemctl enable lxc
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

LXC基于如下内核特性：

* [Kernel Namespace](namespace.md)
* [CGroups](cgroup.md)
* [Chroots (using pivort_root)](chroot.md)
* [Apparmor and SELinux profiles](apparmor_and_selinux.md)
* [Seccomp policies](seccomp.md)
* [Kernel Capabilities](capabilities.md)

> 引申阅读[Linux Security Module](lsm.md)

----------------------------------------

## 使用LXD

lxd-3.0支持到2023年。 lxd用go语言实现。

#### 安装LXD

```
yum install yum-plugin-copr epel-release
yum copr enable ngompa/snapcore-el7
yum install snapd
systemctl enable --now snapd.socket

# Configure the kernel
grubby --args="user_namespace.enable=1" --update-kernel="$(grubby --default-kernel)"
grubby --args="namespace.unpriv_enable=1" --update-kernel="$(grubby --default-kernel)"
echo "user.max_user_namespace=3883" > /etc/sysctl.d/99-userns.conf

# Install the LXD snap
snap install lxd

# Configure LXD
lxd init
```
#### 使用LXD  


