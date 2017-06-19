# 分析QEMU/KVM

KVM(Kernel-based Virtual Machine)是Linux内核中，基于`Intel VT-x`或`AMD-v`技术实现的虚拟化技术。实际上`KVM`虚拟化环境，由两部分组成：位于内核的`kvm.ko`模块，以及位于用户空间的`QEMU`工具。

