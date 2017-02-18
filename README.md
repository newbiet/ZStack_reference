+++++# 

# 

# ZStack\_refer

## 文档目的

本文档主要介绍Mevoco的各个资源以及每个资源状态变化的条件。用户可以在文档中找到Mevoco中所有功能的底层逻辑，对每个资源的操作有清楚的认识。此外，在使用Mevoco的过程中出现问题时，能根据本文档中的线索找到问题的源头和解决方案。

# 引言

产品手册里会详细介绍Mevoco的各个资源的操作、使用场景和错误处理。  
资源章节是Mevoco产品手册的核心，各个资源作为一小节，每个小节还会划分为以下几个部分：

**状态：**每个资源从被创建起，就会具有某种状态，直至这个资源彻底被删除。

**操作：**任何一个资源从一种状态到另一种状态的变化，我们对操作的具体描述分为以下几个部分：

> 注意：操作中的状态包含但不限于**状态**中所述情况。对于一种资源，它的权限更改或者与另一种操作的关联均认为是状态的变化。

* 描述：对这个操作的简单叙述。
* 初始状态：执行操作前，该资源所处的状态。
* 条件：满足执行该操作所必须的环境因素，它不因本操作而发生改变，通常指的是资源间的某种关系。
* 参数：直接参与本操作的某些资源及其状态。
* 结束状态：操作完成后，该资源所处的状态。
* 错误：在满足以上条件和参数的情况下，由于系统或硬件资源所产生的错误，而致使本操作失败。每个错误对应存储错误处理的一个小节。
* 场景：因为其他原因导致的操作异常的情况。每个场景会在场景的一个小节详细阐述。

**标签：**标签是一种特殊的资源，它可以与每种资源进行关联，引入额外的资源属性。

## 读者对象

本文档详述了Mevoco云系统部署的安装、使用教程。本文档主要适用于以下读者：

* 技术支持工程师
* 部署运维工程师
* 产品咨询工程师
* 对Mevoco有兴趣研究的相关人员

## 名词解释

| 术语 | 概念 |
| --- | --- |
| 区域 | 一个区域是由类似主存储，集群，L2网络的资源组成的逻辑组; 它定义一个可见的边界，在相同区域中的资源互相可见并且可以形成某种关系，但在不同区域中的资源是不行的. 例如, 区域A中的一个主存储可以挂载到区域A中的一个集群，但不能挂载到区域B的集群上. |
| 集群 | 一个集群是类似主机（Host）组成的逻辑组. 在同一个集群中的主机必须安装相同的操作系统（虚拟机管理程序,hypervisor）, 拥有相同的二层网络连接, 可以访问相同的主存储. 在实际的数据中心, 一个集群通常对应一个机架（rack） |
| 物理机 | 也称之为物理机，为云主机实例提供计算、内存、网络、存储的物理主机。虽然可以添加管理节点为一个计算节点，但不建议在生产环境中这么部署 |
| 主存储 | 用于存储云主机的磁盘文件的存储服务器。支持本地存储、NFS、Ceph、Fusionstor、Shared Mount Point等类型 |
| 二层网络 | 计算节点的物理网卡设备名称，例如eth0 |
| 三层网络 | 云主机使用的网络配置，包括IP地址范围，网关，DNS等 |
| 镜像 | 云主机所使用的镜像模板文件，包含了云主机的操作系统，也可以定制安装相应的软件 |
| 镜像服务器 | 也称之为备份存储服务器，存储云主机镜像文件的物理主机。建议单独部署镜像服务器 |
| 云盘 | 云主机的数据盘，给云主机提供额外的存储空间，一块云盘在同一时刻只能挂载到一个云主机。一个云主机最多可以挂载24块云盘 |
| 云盘规格 | 创建云盘容量大小的规格定义 |
| 计算规格 | 启动云主机涉及到的CPU数量、内存、网络设置等规格定义 |
| 云主机 | Mevoco 特制虚拟机，即运行在物理机上的虚拟机实例，具有独立的IP地址，可以安装部署应用服务 |
| 安全组 | 针对云主机进行第三层网络的防火墙控制，对IP地址、网络包类型或网络包流向等可以设置不同的安全规则 |
| 标签 | 为资源引入额外的属性，执行特殊的业务逻辑. |



