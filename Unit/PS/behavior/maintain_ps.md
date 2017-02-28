# 停用主存储


主存储进入维护模式之后：
1.创建快照不支持
2.删除快照不支持
3.恢复快照不支持
4.创建云盘支持非实例化云盘创建
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_crt_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_crt_vol.py

5.删除云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_del_attached_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_del_attached_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_del_vol.py

6.恢复云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_recover_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_recover_vol.py

7.挂载云盘不支持
8.卸载云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_maintain_ps_detach_vol.py

9.彻底删除云盘不支持,特别的，如果删除云盘的策略是直接删除的情况下，行为有待细化。
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


对于普通账户和用户，主存储在维护状态的行为定义为：

