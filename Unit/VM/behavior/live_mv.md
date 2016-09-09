# 虚拟机热迁移

* ### 描述

 将云主机从一台物理机迁移到另一台物理机，此过程中云主机一直保持运行状态

* ### 初始状态

 [running](/Unit/VM/status.md)

* ### 前提条件

 1. 目标物理机处于enabled状态，connectted状态
 2. 主存储为共享存储
 3. 云主机所挂载的L3所在的L2，挂载在目标物理机所在集群

* ### 参数

  | 资源 | 状态 |
  | --- | --- |
  | [云主机](/Unit/VM/README.md) | state：running | 
  | [物理机](/Unit/Host/README.md) | state:Enabled ; status:Connected |

* ### 结束状态

 [running](/Unit/VM/status.md)

* ### 错误

* ### 场景

