# 使用Libvirt

Libvirt是使用最广泛的虚拟机管理库，提供虚拟机的管理工具（virsh）以及编程接口。

#### 命令行工具virsh

常用命令：
| 命令 				| 作用 	|
| ----------------- | ---------------		|
| virsh help 		| 显示命令帮助信息 		|
| virsh version 	| 显示版本信息 			|
| virsh list 		| 显示当前运行的VM		|
| virsh console ID 	| 连接指定VM的串口 		|
| virsh dumpxml ID 	| 输出指定VM的XML配置文件 |
| virsh create XML_FILE 	| 用指定的XML配置文件，创建并启动VM	|

#### 虚机配置XML文件

Libvirt库使用的虚拟机的配置文件

+ 设置虚机的CPU

+ 设置虚机的内存

+ 设置虚机的存储设备

+ 设置虚机的网络接口

#### 常用编程接口


