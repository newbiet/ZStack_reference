# 用户标签
用户可以在他们所拥有的资源上创建用户标签，这对于管理相似资源的聚集特别有用; 例如, 用户可以为作为网页服务器(Web Server)的虚拟机设置一个标签’web’:

`CreateUserTag resourceType=VmInstanceVO resourceUuid=613af3fe005914c1643a15c36fd578c6 tag=web
CreateUserTag resourceType=VmInstanceVO resourceUuid=5eb55c39db015c1782c7d814900a9609 tag=web
CreateUserTag resourceType=VmInstanceVO resourceUuid=0cd1ef8c9b9e0ba82e0cc9cc17226a26 tag=web
`

之后, 可以通过:ref:`Query API with tags <query with tags>`来获取这些虚拟机:

`QueryVmInstance __userTag__=web`


用户也可以通过用户标签和系统标签（system tags）合作来改变ZStack的业务逻辑; 例如, 用户可能想在所有作为网页服务器的虚拟机上在一个特定的通过SSD提高IO性能的主存储上创建他们的根存储云盘（root volumes）; 要达到这个目的, 用户可以在主存储上创建一个用户标签’forWebTierVM’:

`CreateUserTag tag=forWebTierVM resourceType=PrimaryStorageVO resourceUuid=6572ce44c3f6422d8063b0fb262cbc62
`

然后在计算规格(instance offering)上创建一个系统标签:

`CreateSystemTag tag=primaryStorage::allocator::userTag::forWebTierVM resourceType=InstanceOfferingVO resourceUuid=8f69ef6c2c444cdf8c019fa0969d56a5
`

这样, 当用户创建通过计算规格`[uuid:8f69ef6c2c444cdf8c019fa0969d56a5]`创建虚拟机的, ZStack会保证虚拟机的根存储云盘都会被创建在拥有用户标签’forWebTierVM’的主存储上， 在这个例子中, 这个主存储的UUID为`6572ce44c3f6422d8063b0fb262cbc62`.