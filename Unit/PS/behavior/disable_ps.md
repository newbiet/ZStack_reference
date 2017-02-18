# 停用主存储

将主存储至于disable状态

#条件


# 场景 1
~~### 测试点~~
1.创建快照，不支持。
：：
    case :  
    
：：
    case :  

：：
    issue :  


2.删除快照，支持
：：
    case :  











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


停用主存储之后：
1. 创建快照不支持
2. 删除快照支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_del_snapshot.py

3. 恢复快照支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_use_snapshot.py

4. 创建云盘支持非实例化云盘创建
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_crt_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_crt_vol.py

5. 删除云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_del_attached_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_del_attached_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_del_vol.py

6. 恢复云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_recover_share_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_recover_vol.py

7. 挂载云盘支持已实例化云盘挂载
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_attach_vol.py

8. 卸载云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_detach_share_vol.py

9. 彻底删除云盘支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_expunge_attached_vol.py
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_expunge_vol.py

10.删除云主机支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_del_vm.py

11.彻底删除云主机支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_expunge_vm.py

12.暂停云主机支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_suspend_vm.py

13.恢复云主机支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_suspend_resume_vm.py

14.加载ISO支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_attach_iso.py

14.卸载ISO支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_detach_iso.py

16.加载网络支持
17.卸载网络支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/virtualrouter/ps/test_disable_ps_attach_remove_nic.py

18.克隆不支持
19.在线创建镜像不支持
20.关机创建镜像不支持
21.指定物理机启动不支持
22.冷迁移云主机不支持
23.在线迁移云主机支持
::
    case=https://github.com/zstackio/zstack-woodpecker/blob/master/integrationtest/vm/multihosts/ps/test_disable_ps_live_migrate.py

24.重置云主机不支持
25.是否支持修改CPU和memory？之后再重启云主机？


对于普通账户和用户，主存储禁用状态的行为定义为：
