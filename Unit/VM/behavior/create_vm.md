# 从ISO创建云主机

* ### 描述

如果您的环境中没有任何其他云主机具有您正在查找的要求（如某个特定的操作系统或硬件配置），则您可以创建单个云主机。在不使用模板或克隆的情况下创建云主机时，可以对虚拟硬件（包括处理器、硬盘和内存）进行配置。


* ### 初始状态
    无
* ### 条件
 1. 物理机所在的集群已加载主存储，主存储状态可用
 2. 物理机所在的集群已加载L2网络，L2网络状态可用
 3. 
 4. 
* ### 参数
 | 单元 | 状态 |
| ---| ---| 
| [镜像](/Unit/Image/README.md) |state:Enabled ; status:Ready|
| [物理机](/Unit/Host/README.md)|state:Enabled ; status:Connected|
| [计算规格](/Unit/Compute_Offering/README.md) | state:Enable |
| [云盘规格](/Unit/Volume_Offering/README.md) | state:Enable |
| [L3网络](/Unit/L3/README.md) | state:Enable |

* ### 结束状态
云主机处于[运行状态](/Unit/VM/status.md)，打开console进入系统引导

* ### 场景

 1. 物理机可用计算资源满足计算规格
 2. 主存储可用磁盘资源满足磁盘规格
 3. L3网络有可用IP