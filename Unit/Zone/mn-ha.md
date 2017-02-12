# 功能描述


# 条件


# 

* 硬件部分：至少三台物理机，统一使用一个共享存储，所有物理机使用我们封装的系统镜像安装
* 软件部分：包含有Mevoco和全套相关软件的虚拟机镜像，MN-VM的控制和代理通信工具z，分布式控制软件Consul和相关的脚本
* 分布式控制机制：在所有的物理机上，选出至少三台物理主机承担管理节点高可用任务，部署Server模式的Consul。与Consul通信的方式：启动时直接使用命令，之后使用HTTP API。Consul Cluster在加入的Consul Server数量符合要求后会自动选出一个Leader，z通过HTTP API向任意一个Consul节点询问当前的Leader，在Leader物理机上启动MN-VM。
* 超时与故障机制：1、正常情况下由Consul Cluster自行选出Leader进行操作，因为网络问题等，导致Leader发生变动，由z做出相应的操作（在当前机器停止MN-VM，在新Leader上启动MN-VM）。2、如果z发现MN-VM在物理机上失效，则做出相应的重启操作。3、如果z发现MN-VM无法正常访问这个统一的共享存储，则由z向Consul Cluster发送命令，将本机的Consul Server下线。
* Live Migration：如果有特殊要求需要迁移MN-VM（比如说维护其中一个物理机）。此时需要强行设定迁移目标的物理机为Leader。
* 管理节点内容：Mevoco和相关的MySQL、RabbitMQ等软件统一运行于一个虚拟机中，类似于目前的单节点部署。
* 管理节点运行和控制：管理节点运行于一个虚拟机中，该虚拟机的磁盘文件存放于共享存储中。管理节点由Consul集群，通过一些控制脚本和我们的z，控制整个生命周期。
* 健康检查：依赖于Consul提供的Health Check机制，编写并注册相关的脚本，需要考虑使用Mevoco API还是注入QGA代理检查
* 节点失效后警报：需要外部监控
* 添加新物理HA节点：通过Consul的Join命令将新物理机上的Consul Server加入到已有的集群。
* 资源保留：所有的物理机上都需要各自保留足够MN-VM运行的计算资源（CPU、Mem）
* Consul升级机制：自身提供了优秀的热升级方案。
* MN-VM升级机制：单独升级内部的Mevoco、RabbitMQ、MySQL等内容。（VMWare的方案为：配置数据等和程序分离）
* z升级机制：替换运行即可。


# 依赖

* 使用我们定制的虚拟机镜像运行管理节点 
* 需要一个管理节点虚拟机的控制和代理通信工具（暂命名为z）
* 需要使用Consul
* 存储必须为共享存储

# 测试

1. 覆盖单节点物理机失效场景
2. 覆盖单节点物理机有效，Mevoco失效的场景

# UI

无UI改动

# 其他

1. Bug/Feature链接
https://github.com/zxwing/premium/issues/1506

2. 尚未考虑的内容
日志和相关数据的长期存储
过期日志和相关数据的清理流程


