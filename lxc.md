# 使用LXC(Linux Container)

主机平台使用CentOS7，使用lxd-3.0（因为lxc-1.0只支持到2019年，lxd-3.0支持到2023年）, lxd用go语言实现。

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


