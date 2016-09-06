# 标签

### 用户标签

用户可以使用`resourceType=VmInstanceVO`在虚拟机上创建用户标签. 

### 系统标签

HostName用户可以为一个虚拟机的默认L3网络指定一个主机名. 这个标签通常在调用`CreateVmInstance`时在*systemTags*参数中指定; 如果默认的L3网络有DNS域, 虚拟机操作系统收到的主机名会自动使用这个DNS域扩展. 例如, 假设主机名为’web-server’ 并且默认L3网络的DNS域为’zstack.org’, 那么最终的机器名将会是’web-server.zstack.org’.

| 标签 | 描述 | 示例 | 起始支持版本
| --- | 
| hostname::{hostname}	| 默认L3网络的机器名 | hostname::web-server | 0.6
例如:

`CreateVmInstance name=vm systemTags=hostname::vm1 imageUuid=d720ff0c60ee48d3a2e6263dd3e12c33 instanceOfferingUuid=76789b62aeb542a5b4b8b8488fbaced2 l3NetworkUuids=37d3c4a1e2f14a1c8316a23531e62988,05266285f96245f096f3b7dce671991d defaultL3NetworkUuid=05266285f96245f096f3b7dce671991d
Next  Previous`
