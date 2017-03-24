#添加主存储
1.添加shared mount point主存储时，如果对应的物理机中主存储的mount path不存在，会抛出对应的错误信息。
2.添加shared mount point主存储时，对应的host中主存储的mount path不存在，会抛出对应的错误信息。
3.在NFS环境下，一个集群下有两台物理机，一台iptables允许连接，一台被iptables禁止连接，此时想挂载主存储，主存储可以添加成功。