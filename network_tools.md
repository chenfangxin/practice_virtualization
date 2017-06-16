# 使用网络工具

为了设置虚拟机运行的外部网络环境，需要在HOST中使用一些网络工具，主要的网络工具为`ip`，`brctl`和`openvswitch`。

#### 使用`ip`命令


#### 使用`brctl`命令

`brctl`是管理网桥的工具, 常用方法如下：

| 命令 | 作用 |
| -----------------------	| ------------ |
| brctl show 				| 显示当前系统中的网桥	 		|
| brctl addbr BRNAME 		| 创建一个网桥 					|
| brctl addif BRNAME IFNAME | 将指定接口添加到指定的网桥中 	|
| brctl delif BRNAME IFNAME | 从指定网桥中删除指定接口 	|
| brctl delbr BRNAME 		| 删除指定的网桥		 	|

#### 使用`openvswitch`

`openvswitch`是最常用的虚拟交换机，用于连接虚拟机和物理网络设备。

| 命令 | 作用 |
| ------------------------- | ---------------- |
| ovs-vsctl show 			|	|
| ovs-vsctl add-br BRNAME 	|	|
