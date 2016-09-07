# 从ISO创建云主机

* ### 描述
使用ISO类型的镜像创建云主机

* ### 初始状态

  [无](/Unit/VM/status.md)

* ### 条件

  1. 物理机所在的集群已加载主存储，主存储状态可用
  2. 物理机所在的集群已加载L2网络，L2网络状态可用 
  3. 物理机所在的Zone已加载镜像服务器
  4. 镜像服务器与主存储类型匹配 
  5. 用户拥有创建云主机权限，拥有对以下参数的使用权限

* ### 参数


  | 资源 | 状态 |
  | --- | --- |
  | [镜像](/Unit/Image/README.md) | state:Enabled ; status:Ready |
  | [物理机](/Unit/Host/README.md) | state:Enabled ; status:Connected |
  | [计算规格](/Unit/Compute_Offering/README.md) | state:Enable |
  | [云盘规格](/Unit/Volume_Offering/README.md) | state:Enable |
  | [L3网络](/Unit/L3/README.md) | state:Enable |

* ### 结束状态

 running

* ### 错误

  1. 云主机创建失败
    * 物理机可用计算资源不满足计算规格
    * 主存储可用磁盘资源不满足磁盘规格
    * L3网络有可用IP

  2. 云主机启动失败
    * 为云主机分配资源满足操作系统

* ### 场景
 
 [ 场景1](/Scenes/PS_localstorage_create_vm.md)：当第一次从localstorage类型的主存储中创建云主机时，云主机创建速度较慢。


