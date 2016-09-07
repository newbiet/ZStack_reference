# 标签

### 用户标签

管理员可以使用resourceType=HostVO在主机上创建用户标签. 例如:

`
CreateUserTag tag=largeMemoryHost resourceUuid=0a9f95a659444848846b5118e15bff32 resourceType=HostVO
`
### 系统标签（System Tags）

主机容量保留（Host Capacity Reservation）
管理员可以使用系统标签在主机上保留一部分内存供系统软件使用. ZStack提供了各种系统标签和全局配置， 以达到更好粒度的内存保留策略控制:

**Hypervisor Global Level:**

如果没有其他层次的配置，全局等级配置(global level) :ref:`kvm.reservedMemory`会应用到所有的KVM主机.

**Zone Level:**

请参见 zone host::reservedMemory; 如果没有其他层次的配置，这个系统标签的值会应用到所有这个区域中的主机上. 这个值覆盖全局配置等级(global level).

** 管理员可以使用resourceType=HostVO在主机上创建用户标签. 例如:CreateUserTag tag=largeMemoryHost resourceUuid=0a9f95a659444848846b5118e15bff32 resourceType=HostVO 系统标签（System Tags）主机容量保留（Host Capacity Reservation）

管理员可以使用系统标签在主机上保留一部分内存供系统软件使用. ZStack提供了各种系统标签和全局配置， 以达到更好粒度的内存保留策略控制:

**Hypervisor Global Level:**

如果没有其他层次的配置，全局等级配置(global level) :ref:`kvm.reservedMemory`会应用到所有的KVM主机.

**Zone Level:**

请参见 zone host::reservedMemory; 如果没有其他层次的配置，这个系统标签的值会应用到所有这个区域中的主机上. 这个值覆盖全局配置等级(global level).

**Cluster Level:**

请参见 cluster host::reservedMemory; 如果没有主机层次的配置，这个系统标签的值会应用到所有这个集群中的主机上. 这个值覆盖区域等级配置（zone level)和全局等级配置（global level）.

**Host Level:**

| 标签 | 描述 | 示例 | 
| --- | ---
| reservedMemory::{capacity} | 这个主机上保留的内存. | reservedMemory::1G

这个配置覆盖所有上面的配置等级.

例如, 假设你还有三个KVM主机zone1->cluster1->{host1, host2, host3}; 默认的内存保留被默认为512M的全局配置（global configuration）:ref:`kvm.reservedMemory`控制; 这时如果在zone1上创建一个系统标签 host::reservedMemory::1G, 所有3个主机的内存保留都会被变成1G; 这时如果再在cluster1 上创建一个系统标签*host::reservedMemory::2G*, 所有3个主机的内存保留都会变成2G; 最后, 如果你在host1上创建一个系统标签*reservedMemory::3G*, 这时host1的内存保留将变成3G，但host2和host3还是2G.

**主机元数据信息（Host Meta Data Information）**

| 标签	| 描述	|示例	|起始支持版本
| --- |
|capability:liveSnapshot	|如果标签存在, 主机上的虚拟机管理程序支持在线云盘快照（live volume snapshot）	|capability:liveSnapshot	
| os::distribution::{distribution} |主机的操作系统提供商 |os::distribution::Ubuntu
|os::release::{release}	 | 主机的操作系统发布版本	 | os::release::trusty	
|os::version::{version}	| 主机的操作系统版本	|os::version::14.04	

**KVM主机元数据信息（KVM Host Meta Data Information）**

| 标签	| 描述	| 示例	
| ---| 
| qemu-img::version::{version}	| qemu-img 版本	|qemu-img::version::2.0.0	
| libvirt::version::{version}	| libvirt 版本	| libvirt::version::1.2.2	
| hvm::{flag}	| 主机硬件虚拟化标识（host hardware virtualization flag）; vmx表示Intel CPU; | svm表示AMD CPU	hvm::vmx


