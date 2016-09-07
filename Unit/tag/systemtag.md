# 系统标签

系统标签相比用户标签有更广泛的用途; 就像上一节中的例子一样，用户可以使用它们来指导ZStack执行特殊的业务逻辑. 扩展ZStack功能的插件（Plugins）可以通过使用系统标签来引入额外的资源属性, 或记录和资源紧密相关的元数据.

例如, 要想在KVM主机上实施在线迁移（live migration）或者在线快照（live snapshot）, ZStack需要知道KVM主机的libvirt版本和QEMU版本，这些信息都是元数据 因此ZStack将他们作为主机的系统标签存储起来. 例如, 管理员可以通过下面的命令查看一个KVM主机的系统标签:

`QuerySystemTag fields=tag resourceUuid=d07066c4de02404a948772e131139eb4`

*d07066c4de02404a948772e131139eb4*是某个云主机的UUID, 查询结果为:

{ "inventories": [ 

{ "tag": "capability:liveSnapshot" },

 { "tag": "qemu-img::version::2.0.0" },

 { "tag": "os::version::14.04" },

 { "tag": "libvirt::version::1.2.2" },

 { "tag": "os::release::trusty" },

 { "tag": "os::distribution::Ubuntu" } ], 

"success": true }

这一类的系统标签, 被称为内部系统标签（inherent system tags）; 内部系统标签只能被ZStack的服务（services）或插件（plugins）创建, 并且不能被DeleteTag API删除.

为了增加新的功能, 插件通常需要为一个资源添加新的属性; 虽然插件不能通过改变一个资源的数据库模式（database schema）来增加一个新的列（column） , 但它可以为一个资源创建作为系统标签的新属性. 例如, 当创建一个虚拟机时, 用户可以为云主机某L3网络上的网卡绑定一个可以通过网络访问的机器名（hostname）:

`CreateVmInstance name=testTag systemTags=hostname::web-server-1 l3NetworkUuids=6572ce44c3f6422d8063b0fb262cbc62 instanceOfferingUuid=04b5419ca3134885be90a48e372d3895 imageUuid=f1205825ec405cd3f2d259730d47d1d8`

这个机器名被实现为一个系统标签; 如果你查看 VM inventory in chapter ‘Virtual Machine’, 那里没有叫做’hostname’的属性; 然而, 你可以在 虚拟机的系统标签中发现它:

`QuerySystemTag fields=tag,uuid resourceUuid=76e119bf9e16461aaf3d1b47c645c7b7
`
```
{ "inventories": [ 
{ "tag": "hostname::web-server-1", "uuid": 

"596070a6276746edbf0f54ef721f654e"

 } 
], 
"success": true }
```

这类系统标签就是非内部的（non-inherent）, 用户可以通过DeleteTag删除它; 例如, 如果用户想把一个之前的虚拟机的机器名更改为 ‘web-server-nginx’, 可以这样做:

`DeleteTag uuid=596070a6276746edbf0f54ef721f654e`

`CreateSystemTag resourceType=VmInstanceVO tag=hostname::web-server-nginx resourceUuid=76e119bf9e16461aaf3d1b47c645c7b7`

停止和启动虚拟机之后, 虚拟机中的系统（guest operating system）会接受到’web-server-nginx’作为新的机器名.
