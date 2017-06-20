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

Libvirt中每个虚机称为一个`domain`，虚拟机的配置文件格式详见[Domain XML](http://libvirt.org/formatdomain.html)。

在这个配置文件中，有一个根标签`<domain>`，所有虚机相关的配置，都封装在子标签中，例如：

```
<domain type='kvm'>
	<name>T1_TSOS</name>
	<os>
		<type arch='x86_64'>hvm</type>
		<boot dev='hd'/>
	</os>
</domain>
```

+ 设置虚机的CPU

设定虚拟机的CPU个数，以及每个虚机CPU对应的线程所绑定的物理CPU，如下：

```
	<vcpu placement='static'>2</vcpu>
	<cputune>
		<vcpupin vcpu='0' cpuset='0'/>
		<vcpupin vcpu='1' cpuset='1'/>
	</cputune>
```

+ 设置虚机的内存

设定内存大小以及特性：

```
	<currentMemory unit='GiB'>4</currentMemory>
	<memoryBacking>
		<hugepages/>
	</memoryBacking>
```

+ 设置虚机的硬件设备

虚机使用的设备，放在`<device>`子标签中描述,主要由存储设备，网络接口，串口等。

++ 设置虚机的存储设备

存储设备放在二级标签`<disk>`中，示例如下：

```
	<disk type='file' device='disk'>
		<driver name='qemu' type='qcow2'>
		<source file='/root/workplane/T1_TSOS.qcow2'/>
		<target dev='hda' bus='ide'>
	</disk>
```

++ 设置虚机的网络接口

虚机使用的网络接口，可以由多种实现方式，比如全虚拟型，半虚拟型以及硬件直通型等。全虚拟/半虚拟型网络接口的实现，分为前端(Frontend)和后端(Backend)，前端就是虚机系统看到的设备，后端设备是`Hypervisor`中看到的设备。前端设备的描述放在`<interface>`二级标签中，如下：

```
<interface type='bridge'>
	<mac address='52:54:00:f3:6a:f3'/>
	<source bridge='br0'>
	<model type='e1000'/>
</interface>
```

以上标签是将后端网络设备连接在Linux桥`br0`上，若后端要连接在OVS上，或在DPDK加速的OVS上，其描述有所不同。


直通模式是将`Hypervisor`中的设备直接交给虚机管理，使用`<hostdev>`标签描述，如下：

```
<hostdev mode='subsystem' type='pci' managed='yes'>
	<source>
		<address type='pci' domain='0x0000' bus='0x03' slot='0x10' function='0x0'/>
	</source>
</hostdev>
```

#### 常用编程接口


