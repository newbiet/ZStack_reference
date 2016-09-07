# 标签

### 用户标签

用户可以使用resourceType=InstanceOfferingVO在计算规格上创建用户标签. 例如:

CreateUserTag resourceType=InstanceOfferingVO tag=web-server-offering resourceUuid=45f909969ce24865b1bbca4


### 系统标签

当创建虚拟机的时候, 用户可以通过系统标签指定从哪个主存储创建根云盘.

| 标签| 描述 | 示例 | 
| --- | 
| primaryStorage::allocator::uuid::{uuid} | 如果该标签存在, 虚拟机的根云盘会从*uuid*指定的主存储分配;如果指定的主存储不存在或没有足够的容量，会报告分配失败（allocation failure）.|primaryStorage::allocator::uuid::b8398e8b7ff24527a3b81dc4bc64d974	
|primaryStorage::allocator::userTag::{tag}::required | 如果该标签存在, 虚拟机的根云盘会从带有用户标签*tag*的主存储分配;如果指定的主存储不存在或没有足够的容量，会报告分配失败（allocation failure) |primaryStorage::allocator::userTag::SSD::required |
| primaryStorage::allocator::userTag::{tag} | 如果该标签存在, 虚拟机的根云盘会首相尝试从带有用户标签*tag*的主存储分配, 如果找不到带指定标签的主存储或容量不足，ZStack会随机选择一个主存储分配这个根云盘;| primaryStorage::allocator::userTag::SSD | 

如果在计算规格上有多个上面提到的系统标签存在, 它们的优先顺序是:

`primaryStorage::allocator::uuid::{uuid} > primaryStorage::allocator::userTag::{tag}::required > primaryStorage::allocator::userTag::{tag}
`
