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