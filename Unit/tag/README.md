# 标签

在ZStack配合标签不仅可以帮助用户整合资源，而且还能控制软件的行为。ZStack有完整的标签使用规范配合特殊定义的类别，形式。除了用户，插件可以创建自己的标签，为了记录元数据和扩展现有资源的属性; 通过以上方式，标签可以帮助插件引入新的功能，而无需改变ZStack配合的数据库架构，减少为数据库迁移而需要软件升级。 

## 意义

随着云计算越来越多的资源，用户可能希望有一种方式为相似的一类资源来贴上标签，例如，所有作为Web服务器的虚拟机都带有“web-tier-VM'的标签，以便从UI组或CLI查找他们。对于IaaS的本身，预先定义的业务逻辑不可能满足用户的所有需求。举个创建VM例子，选择目标物理机的默认算法，只是随机挑选了一个来自集群的物理机。但用户可能要适合自己的方案的各种算法; 例如选择的物理机需要大于8G可用内存，选择具有主机SR-IOV的硬件，或选择的物理机已经具有同一用户运行的云主机。IaaS的软件不可能提供所有的无穷的，未知要求的特殊API，必须有让基础的API（如APICreateVmInstanceMsg）附加额外信息的机制。

根据他们的业务逻辑，插件可以选择或不创建数据库模型。例如，开放式的vSwitch L2网络，创建一个新的资源类型，可能需要一个新的模型; 然而，一个插件，允许预留物理机内存可能并不需要创建一个单独的模型，但需要添加一段数据连接到物理机。如果IaaS的软件不提供一种方式来使插件附加数据。那就需要用户创造新的，琐碎的模型或修改现有的模型来增加其列，这会导致由于软件升级的数据库迁移毛茸茸的情况。

使第三方软件的信息能够存储到ZStack的数据库，而不影响数据完整性，并使用ZStack来查询的API。

## 问题

大多数IaaS的软件有标签的概念。然而，并不是所有的人都定义为不同的场景的标签的详尽说明。例如，有的用户使用它来归类用户资源，有的用户也会使用标签内部业务逻辑。需要根据不同的场景仔细的定义每个标记的各个部分。

## 描述

在ZStack配合，标签基本上都是一小段相关联信息的资源字符串。一个标记主要由以下字段：

| 领域 | 描述 |
| --- | --- |
|UUID |	标签的UUID |
| esourceUuid | 该标签与相关的资源UUID |
| esourceType | 为该标签与相关联的资源类型 |
| 标签 | 包含有意义的信息的字符串 |
| 类型 | 标签类型：系统或用户 |

标签为ZStack配合和其他的IaaS软件之间的根本区别是ZStack配合分类标签分为两类：用户和系统。

### 命名规则

用户标签和系统标签最多都只能有2048个字符.

对于用户标签, 没有强制的命名约定, 推荐使用可读的有意义的字符串.

对于系统标签, 和ZStack中服务和插件定义的一样, 使用 :: 作为分隔符（delimiters）.


### 资源类型（Resource Type）

|资源类型 | 
| --- |
| ZoneVO |
| ClusterVO |
| HostVO
| PrimaryStorageVO
| BackupStorageVO
| ImageVO
| InstanceOfferingVO
| DiskOfferingVO
| VolumeVO
| L2NetworkVO
| L3NetworkVO
| IpRangeVO
| VipVO
| EipVO
| VmInstanceVO
|VmNicVO
| SecurityGroupRuleVO
| SecurityGroupVO
|PortForwardingRuleVO
| VolumeSnapshotTreeVO
| VolumeSnapshotVO

