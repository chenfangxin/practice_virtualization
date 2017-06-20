# 临界指令和Ring Deprivileging

实现OS级别虚拟化的一般思路是让`GUEST OS`运行在非特权级，当`GUEST OS`执行了需要在特权级中运行的指令（敏感指令）时，CPU会产生`trap`，从而被`Hypervisor`捕获并处理。x86平台上，在非特权级执行某些敏感指令并不产生`trap`，这些指令称为临界指令，这导致在x86平台实现虚拟化非常困难。


除了`临界指令`，`Ring Deprivileging`是在x86平台上实现虚拟化面临的主要问题，具体分为如下几个方面：

+ `Ring Compression`

+ `Ring Alias`

+ `Nonfaulting access to privileged state`

+ `Address Space Compression`

+ `Adverse impacts on guest transition`

+ `Interrupt Virtualization`

+ `Access to hidden state`

