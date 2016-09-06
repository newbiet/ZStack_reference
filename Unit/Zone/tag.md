# 标签
### 用户标签
管理员可以在一个区域上用resourceType=ZoneVO创建用户标签. 

例如:
`CreateUserTag resourceType=ZoneVO resourceUuid=0cd1ef8c9b9e0ba82e0cc9cc17226a26 tag=privateZone
`

### 系统标签

保留容量（Reserved Capacity）

| 标签（Tag）| 描述 | 示例 |　起始支持版本 |
| --- | ---
| host::reservedMemory::{capacity} | 请参见 主机容量保留（Host Capaci=pk=-8ty Reservation）| host::reservedMemory::1G |　0.6