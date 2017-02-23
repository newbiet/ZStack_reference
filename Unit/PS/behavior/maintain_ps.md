# 停用主存储

|PS|disable（不使用PS新的资源的操作都支持）|maintain（跟PS有关的操作都不支持）|
|------|------|------|
|创建快照|不支持|不支持|
|删除快照|支持|不支持|
|恢复快照|支持|不支持|
|创建云盘|支持非实例化云盘创建|支持非实例化云盘创建|
|删除云盘|支持|支持|
|恢复云盘|支持|支持|
|挂载云盘|支持已实例化云盘挂载|不支持|
|卸载云盘|支持|支持|
|彻底删除云盘|支持|不支持|
|删除云主机|支持|支持|
|彻底删除云主机|支持|不支持|
|暂停云主机|支持|N/A|
|恢复云主机|支持|N/A|
|加载ISO|支持|支持|
|卸载ISO|支持|支持|
|加载网络|支持|N/A|
|卸载网络|支持|N/A|
|克隆|不支持|不支持|
|在线创建镜像|不支持|N/A|
|关机创建镜像|不支持|不支持|
|指定物理机启动|不支持|不支持|
|冷迁移云主机|不支持|不支持|
|在线迁移云主机|支持|N/A|
|重置云主机|不支持|不支持|


主存储进入维护模式之后：
1. 创建快照不支持
2. 删除快照不支持
3. 恢复快照不支持
4. 创建云盘支持非实例化云盘创建
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_crt_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_crt_vol.py

5. 删除云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_del_attached_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_del_attached_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_del_vol.py

6. 恢复云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_recover_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_recover_vol.py

7. 挂载云盘不支持
8. 卸载云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_detach_vol.py

9. 彻底删除云盘不支持,特别的，如果删除云盘的策略是直接删除的情况下，行为有待细化。
10.删除云主机支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_del_vm.py

11.彻底删除云主机不支持
12.暂停云主机N/A
13.恢复云主机N/A
14.加载ISO支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_attach_iso.py

14.卸载ISO支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_detach_iso.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_detach_share_vol.py

16.加载网络N/A
17.卸载网络N/A
18.克隆不支持
19.在线创建镜像N/A
20.关机创建镜像不支持
21.指定物理机启动不支持
22.冷迁移云主机不支持
23.在线迁移云主机N/A
24.重置云主机不支持
