# 虚拟机热迁移

* ### 描述

 将云主机从一台物理机迁移到另一台物理机，此过程中物理机一直保持运行状态

* ### 初始状态

 [running](/Unit/VM/status.md)

* ### 前提条件

 

* ### 参数

  | 资源 | 状态 |
  | --- | --- |
  | [镜像](/Unit/Image/README.md) | state:Enabled ; status:Ready |
  | [物理机](/Unit/Host/README.md) | state:Enabled ; status:Connected |
  | [计算规格](/Unit/Compute_Offering/README.md) | state:Enable |
  | [云盘规格](/Unit/Volume_Offering/README.md) | state:Enable |
  | [L3网络](/Unit/L3/README.md) | state:Enable |

* ### 结束状态

[running](/Unit/VM/status.md)

* ### 错误

* ### 场景

