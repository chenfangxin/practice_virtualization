# 使用LXC(Linux Container)

主机平台使用CentOS7，lxc-1.0支持到2019年，lxc-2.0支持到2021年，lxd-3.0支持到2023年。 lxd用go语言实现。

# 安装LXC

# 使用LXC

# LXC的原理

LXC基于如下内核特性：

* [Kernel Namespace](namespace.md)
* [Apparmor and SELinux profiles](apparmor_and_selinux.md)
* [Seccomp policies](seccomp.md)
* [Chroots (using pivort_root)](chroot.md)
* [Kernel Capabilities](capabilities.md)
* [CGroups](cgroup.md)

----------------------------------------

# 安装LXD

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
# 使用LXD  


