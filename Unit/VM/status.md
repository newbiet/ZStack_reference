# 云主机状态
| 状态 | 描述 |
| --- | --- |
| Created |此状态时，云主机还只是创建于数据库中的一个记录, 并没有在任何的主机上启动. 这个状态仅在创建一个新的虚拟机的时候出现. |
| Starting | 此状态时，云主机正在一个物理机上启动|
| Running | 此状态时，云主机正运行在一个物理机 |
| Stopping | 此状态时，云主机正在一个物理机上停止过程中 |
| Stopped | 此状态时，云主机已经停止，没有运行在任何物理机上 |
| Rebooting | 此状态时，云主机正在被删除 |
| Created | 此状态时，云主机的资源配额已设置，但未分配实际资源 |
| Migrating | 在这种状态时，虚拟机正在被迁移到另一个物理机上 |
| Unknown |由于某些原因, 例如,物理机失接, ZStack不能检查虚拟机的可用状态 
