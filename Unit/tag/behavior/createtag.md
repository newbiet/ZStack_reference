# 创建标签

有两种创建标签的方式; 对于已经创建的资源, 用户可以使用命令 CreateUserTag 或者 CreateSystemTag来创建用户标签或系统标签. 例如:

CreateUserTag resourceType=DiskOfferingVO resourceUuid=50fcc61947f7494db69436ebbbefda34 tag=for-large-DB
CreateSystemTag resourceType=HostVO resourceUuid=50fcc61947f7494db69436ebbbefda34 tag=reservedMemory::1G
对于一个将要被创建的资源, 因为它还没有被创建, 所以没有UUID可以被CreateUserTag和CreateSystemTag命令引用; 在这种情况下, 用户可以使用每个“创建类型的API命令”（creational API command）的*userTags*和*systemTags*域, 在创建时，用户可以通过传递列表的形式定义多个标签; 例如:

CreateVmInstance name=testTag systemTags=hostname::web-server-1
userTags=in-super-data-center,has-public-IP,hot-fix-applied-2015-5-1
l3NetworkUuids=6572ce44c3f6422d8063b0fb262cbc62
instanceOfferingUuid=04b5419ca3134885be90a48e372d3895 imageUuid=f1205825ec405cd3f2d259730d47d1d8