# 标签



###用户标签

用户可以使用resourceType=DiskOfferingVO在云盘规格上创建用户标签. 例如:

`CreateUserTag tag=smallDisk resourceType=DiskOfferingVO resourceUuid=d6c49e73927d40abbfcf13852dc18367`




###系统标签
专用主存储（Dedicated Primary Storage） 

当从云盘规格创建云盘的时候, 用户可以通过系统标签指定从哪个主存储创建云盘.

| 标签 | 描述| 示例 
| ---| 
| primaryStorage::allocator::uuid::{uuid} | 如果该标签存在, 从该云盘规格创建的云盘会从*uuid*指定的主存储分配; 如果指定的主存储不存在或没有足够的容量，会报告分配失败（allocation failure）.| primaryStorage::allocator::uuid::b8398e8b7ff24527a3b81dc4bc64d974 0.6 |
| primaryStorage::allocator::userTag::{tag}::required |如果该标签存在, 从该云盘规格创建的云盘会从带有用户标签*tag*的主存储分配; 如果指定的主存储不存在或没有足够的容量，会报告分配失败（allocation failure）.| primaryStorage::allocator::userTag::SSD::required |
| primaryStorage::allocator::userTag::{tag} | 如果该标签存在, 从该云盘规格创建的云盘会首先尝试从带有用户标签*tag*的主存储分配, 如果找不到带指定标签的主存储或容量不足，ZStack会随机选择一个主存储分配这个云盘.|primaryStorage::allocator::userTag::SSD |

如果在云盘规格上有多个上面提到的系统标签存在, 它们的优先顺序是:

`primaryStorage::allocator::uuid::{uuid} > primaryStorage::allocator::userTag::{tag}::required > primary`


