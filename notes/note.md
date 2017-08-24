DataNode详解
DataNode 类包含了data树中的节点的数据
一个数据节点包含一个对它父节点的引用,
它自己的数据的一个字节数组,
一个ACL数组,
一个stat对象,
一个它的子路径的集合.

dataNode.getChildren返回不可更改的集合

Collections.unmodifiableSet

DataTree详解
这个类维护了树结构的数据.
他没有任何的网络或者客户端连接代码所以他可以被独立的测试.
这个树维护了两个并行的数据结构:
一个 hashtable 它映射了从全路径到数据节点数据节点
和一个树.
所有对一个路径的访问都是通过hashtable.
这个树只有在序列化到磁盘的时候被遍历

nodes(ConcurrentHashMap<String, DataNode>)

什么是acl?

v_0.0.1
### ZookeeperServer.main()
1. 通过构造函数创建 Zookeeper 实例 zk
2. 启动 zk
3. 创建 NIOServerCnxn.Factory 实例 t 
4. 设置 t 的 ZooKeeperServer
5. t 等待 
6. zk 关闭

### 1. 通过构造函数创建 Zookeeper 实例 zk
1. 设置 dataDir/dataLogDir/tickTime/authenticationProviders

### 2. 启动 zk
1. 初始化 dataTree
2. 创建会话追踪器
3. 设置请求处理器
4. 设置 running 的值为 true
5. 调用 notifyAll()

### 3. 创建 NIOServerCnxn.Factory 实例 t 
1. 设置线程的名字为 NIOServerCxn.Factory
2. 设置线程为守护进程
3. 设置成员变量 (ServerSocketChannel) ss
4. 绑定 ss 的 socket 到 端口 port
5. 设置 ss 为 非阻塞的
6. ss 注册 OP_ACCEPT
7. 开始执行

### 4. 设置 t 的 ZooKeeperServer
1. 设置实例变量 (ZooKeeperServer)zks
2. 设置实例变量 (未处理请求数)outstandingLimit
3. 设置zk的 serverCnxnFactory 为 t 的 this