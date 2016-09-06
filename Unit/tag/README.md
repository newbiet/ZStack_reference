# 标签

##标签系统

在ZStack配合标签不仅可以帮助用户整合资源，而且还能控制软件的行为。ZStack有完整的标签使用规范配合特殊定义的类别，形式。除了用户，插件可以创建自己的标签，为了记录元数据和扩展现有资源的属性; 通过以上方式，标签可以帮助插件引入新的功能，而无需改变ZStack配合的数据库架构，减少在软件升级的需求为数据库迁移。 

## 意义

随着云计算越来越多的资源，用户可能希望的方式与人类可读标签组相似的资源，例如，带有标签“web层-VM'，Web服务器的所有虚拟机，以便检索它们从UI组或CLI。对于IaaS的本身，预先定义的业务逻辑可从未满足用户的要求; 举创建VM作为一个例子，选择目标主机的默认算法可能只是随机挑选了一个来自主机的游泳池，但用户可能要适合自己的方案的各种算法; 如选择的宿主以比8G存储器更多，选择具有主机SR-IOV 的硬件，或选择宿主已经具有同一用户运行的虚拟机。IaaS的软件几乎不能提供所有的无尽的，不可预知的要求个别API，必须有让基地的API（如APICreateVmInstanceMsg）进行额外信息的机制。

根据他们的业务逻辑，插件可以选择或不创建数据库模式。例如，开放式的vSwitch L2网络，创建一个新的资源类型，可能需要一个新的模式; 然而，一个插件，允许主机内存的预订可能并不需要创建一个单独的模式，但一个数据连接到主机。如果IaaS的软件不提供一种方式，插件附加数据，他们将开始要么创造新的，琐碎的架构或修改现有的模式来增加其列，这会导致软件升级的数据库迁移毛茸茸的局面。

最后，在ZStack配合内置的第三方软件，使他们能够信息存储到ZStack配合的数据库可避免数据完整性问题，并使用ZStack配合的综合查询的API（详见技术使他们的查询API）。

## 问题

大多数IaaS的软件有标签的概念。然而，并不是所有的人都定义为不同的场景的标签的详尽说明。例如，有些人可能会使用用户资源的聚合，而标签其中的一些可能会使用标签内部业务逻辑。ZStack配合，而是精心设计的定义不同场景的标记每一个方面的规范。

## 标签系统

在ZStack配合，标签基本上都是背着小片的信息相关联的资源字符串。一个标记主要由以下字段：

| 领域 | 描述 |
| --- | --- |
|UUID |	标签的UUID |
| esourceUuid | 该标签与相关的资源UUID |
| esourceType | 为该标签与相关联的资源类型 |
| 标签 | 包含有意义的信息的字符串 |
| 类型 | 标签类型：系统或用户 |

标签为ZStack配合和其他的IaaS软件之间的根本区别是ZStack配合分类标签分为两类：用户和系统。

### 命名约定（Name Convention）
用户标签和系统标签最多都只能有2048个字符.

对于用户标签, 没有强制的命名约定, 但推荐使用可读的有意义的字符串.

对于系统标签, 和ZStack中服务和插件定义的一样, 他们使用 :: 作为分隔符（delimiters）.


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

### 1.用户标签

用户标签，因为顾名思义，是由用户提供分组资源创建的标记。例如，分组由一个标签'的Apache2-HTTP“安装的Apache2 HTTP服务器的虚拟机; 然后，用户可以使用带标签“的Apache2-HTTP”查询API作为查询条件检索这些虚拟机：

`QueryVmInstance __userTag__=apache2-http`

这是标签的最常见的用法。资源可以有关联的，在不同的逻辑组分组多个标签。
![png](/images/tag1.png )

与系统附带的标签，用户标签也可以用来控制ZStack配合的行为。例如，如果一个用户标记 SSD已经在一个主存储创建的，一个系统标记可以指示ZStack配合到仅与用户标记主存储创建VM的根卷 SSD。在这种情况下，用户标签更像是用户资源的元数据输入。我们将很快看到该插件还可以使用系统标记创造资源的元数据。

### 2.系统标签

不像可由用户在任何时间任意值来创建用户标签，系统标签，有固定的值格式，是由ZStack配合协调服务和插件预先定义的，并且可以在以下情况下使用：

**2.1 元数据**

插件可以使用系统标签来记录资源的元数据。例如，主机的数据库表没有捕捉到元数据，如虚拟机管理程序版本，虚拟机管理程序的SDK版本列; 但是，衍生的宿主插件，例如，KVM主机插件，可能需要的那些元数据，以便决定是否有些功能适用于当前的管理程序; 例如，KVM的活卷快照可支持由libvirt的和QEMU版本确定。在ZStack配合，在KVM主机插件连接到后端主机时节省了操作系统版本，libvirt的版本，QEMU版本，和QEMU-IMG工具版本系统标记。
```
QuerySystemTag fields=tag resourceUuid=d07066c4de02404a948772e131139eb4


{
  "inventories": [
      {
          "tag": "capability:liveSnapshot"
      },
      {
          "tag": "qemu-img::version::2.0.0"
      },
      {
          "tag": "os::version::14.04"
      },
      {
          "tag": "libvirt::version::1.2.2"
      },
      {
          "tag": "os::release::trusty"
      },
      {
          "tag": "os::distribution::Ubuntu"
      }
  ],
  "success": true
}

```

**2.2资源属性**


插件还可以使用系统标记新的属性添加到资源。例如，虚拟机的数据库模式没有列记录什么分配虚拟机网卡的IP时，分配算法来使用。这种额外的属性可以被实现为系统标记。没有限制系统的数字标记的插件可以创建; 辅助插件可以利用这一点，并避免与数据库模式困扰。

> 数据库模式VS系统标签：由于两个数据库架构和系统变量可以定义资源的属性，它有时令人困惑的属性是否应为数据库模式或单独的表中的系统变量的一列。修改现有的数据库模式，以添加新列通常需要数据库迁移是IaaS的软件升级的主痛苦，使开发人员可能更喜欢系统标记所有新特性。然而，滥用系统标记是一个错误的编程方式。通过ZStack配合的惯例，在系统标签的形式，性质只能用于引进非固有的资源属性; 系统变量没有抢救设计拙劣的数据库模式进行。例如，如果集群UUID从VM的数据库模式缺失（虽然它不会），必须将其加回甚至数据库迁移是必需的，但通过对于私人使用用户做出的插件推出的部门ID应当实施作为一个系统变量。这种权衡的不容易，有时拿，我们将会把目光严格上的任何数据库架构更改。

**2.3元数据编程**


系统变量也可以以影响ZStack配合的执行流，它类似于注释资源元编程莫名其妙。例如，管理员可以创建一个系统变量`reservedMemory::1G`KVM主机上，暗示ZStack配合主机分配到该主机可用内存保留1G内存;

 如果管理员更改他或她的脑海里，他或她可以删除标记返回1G内存当年。有很多类似的系统标签;

 例如，在用户标签部分我们提到用户标签的合作SSD和系统标签指定虚拟机的根卷目的地主存储; 系统变量被称为`primaryStorage::allocator::userTag::{tag}::required`; 如果`primaryStorage::allocator::userTag::SSD::required`是在一个实例提供创建，从该实例提供创建虚拟机的根卷将分配给使用用户标签仅主存储SSD。有许多所谓的`interpreting points`将寻求执行过程中特定系统的标签，它可以改变代码的默认行为。

2.4第三方软件集成

在ZStack配合内置可以使用系统标签存储信息与ZStack配合的数据库资源以及第三方软件; 这是特别有用的，以避免第三方软件的数据库和ZStack配合的数据库中的数据的不一致性。例如，一个私人软件可以记录虚拟机的部门ID对从各部门，这通常是在专用数据库完成IT资源的审核使用，并强制私有软件来跟踪VM生命周期，因为它需要时将VM来更新自己的数据库创建或破坏。否则，数据将错误地反映事实真相。与系统标记的帮助下，私有软件可以使用一个系统标记，例如`audit::departmentId::{id}`，存储在ZStack配合的数据库中的信息，传送用于管理部门ID的生命周期中ZStack配合责任; 当被销毁一个虚拟机，它的部门ID（如`audit::departmentId::1`）将被自动删除VM行的同一数据库事务中删除。此外，私营软件可以通过使用常规查询API仰视他们的部门ID检索虚拟机：

`QueryVmInstance fields=uuid __sysTag__=audit::departmentId::1
`注：在这个版本ZStack配合（0.6），我们还没有打开，允许任意定义系统标记的接口，所有的系统标签是预先定义的。我们计划在打开下一个版本的这个接口，用户自定义的系统变量可以与一些允许的前缀创建，例如，3rd::。
关系到其他组件

标签系统的核心ZStack配合部件中的一个; 它不仅拥有独立的API和服务，而且还可以无缝等核心部件集成在一起。用户可以在正在创建资源的时间创建标记或创建资源之后。所有ZStack配合造物的API支持两个固有参数：userTags和 systemTags在他们通过标签将与资源一起被创建。例如：

`CreateVmInstance name=testTag systemTags=hostname::web-server-1 l3NetworkUuids=6572ce44c3f6422d8063b0fb262cbc62
instanceOfferingUuid=04b5419ca3134885be90a48e372d3895 imageUuid=f1205825ec405cd3f2d259730d47d1d8`

如果资源已经存在，用户可以创建或删除使用标签API标签：

`CreateUserTag resourceType=VmInstanceVO resourceUuid=613af3fe005914c1643a15c36fd578c6 tag=web`

`DeleteTag uuid=596070a6276746edbf0f54ef721f654e`

与资源相关​​的标签时，会被删除该资源被自动删除。

资源可以通过两个特殊查询条件的标签进行查询：`__userTag__`与`__systemTag__`：

`QueryVmInstance __userTag__=web zoneUuid=04b5419ca3134885be90a48e372d3895`

`QueryHost __systemTag__=capability:liveSnapshot`
也有对特定类别查询的API：

`QueryUserTag resourceUuid=0cd1ef8c9b9e0ba82e0cc9cc17226a26 tag~=web-server-%`

`QuerySystemTag resourceUuid=50fcc61947f7494db69436ebbbefda34`


概要

在本文中，我们展示了ZStack配合的标签系统。随着该系统，用户，插件和第三方软件可以使用各种方式无标签代码和数据库架构更改。这又是一个基础，使快速发展的ZStack配合成为一个成熟的，完整的云计算解决方案，同时保持核心业务流程强劲的潜力。