# Kata Container

主页：`https://katacontainers.io`，开发语言：Go

----

kata container本质上是跑在`hypervsior`上的容器，支持OCI(Open Container Initialtive)和Kubernetes CRI(Container Runtime Interface)接口。

> 当利用container实现公有云时，仅仅通过`Cgroup`和`namespace`提供的隔离，安全性还是不够。很多人在VM里设置container，但是这样性能损耗很大。


