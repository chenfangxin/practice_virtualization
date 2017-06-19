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
| ----------------------------------------- | ------------------------- 			|
| ovs-vsctl show 							| 显示当前系统中的虚拟交换机的配置 		|
| ovs-vsctl add-br BRNAME 					| 添加虚拟交换机 						|
| ovs-vsctl add-port BRNAME	PORT			| 将接口加入虚拟交换机					|
| ovs-vsctl list interface PORT				| 显示虚拟交换机的接口信息				|
| 											|										|
| ovs-ofctl show BRNAME						| 显示指定OpenFlow虚拟交换机的配置		|
| ovs-ofctl dump-ports BRNAME				| 显示指定OpenFlow虚拟交互机的端口统计 	|
| ovs-ofctl mod-port BRNAME	PORT up/down 	| 修改端口状态							|
| 											|										|
| ovs-ofctl dump-flows BRNAME				| 显示指定OpenFlow虚拟交换机的流规则 	|
| ovs-ofctl add-flow BRNAME	'OF-RULE'		| 添加OpenFlow流规则					|

