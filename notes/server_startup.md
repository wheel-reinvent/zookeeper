## 启动 zk
1. 初始化 dataTree
2. 创建会话追踪器
3. 设置请求处理器
4. 设置 running 的值为 true
5. 调用 notifyAll()

### 1. 初始化 dataTree
1. 遍历 dataDir 目录中的所有文件从快照中读取最大的 zxid highestZxid
2. 根据 highestZxid 找出最新的快照
3. 快照存在 
 - 解析快照中的信息(dataTree 及 会话和会话的过期时间)
 - 设置 dataTree 的 lastProcessedZxid 为 highestZxid
 - 回放 dataLogDir 目录下 highestZxid 之前对应的日志文件
 - 遍历日志文件做回放,并重新计算 highestZxid 的值
 - 设置实例变量 hzxid 的值 为 highestZxid
3. 快照不存在
 - 初始化会话的Map为空Map
 - 创建dataTree的实例
4. 清理会话(dataTree中存在但是在sessionsWithTimeouts中不存在的会话)
5. 设置 dataTree.initialized 为 true
6. 重新做一次干净的快照

### 2. 创建会话追踪器
1. 调用 SessionTrackerImpl 的构造函数创建实例 sessionTracker
 - 设置线程名称 为 SessionTracker
 - 设置 expirer 为 ZookeeperServer 实例本身
 - 设置 expirationInterval
 - 设置 sessionsWithTimeout
 - 设置 nextExpirationTime
 - 遍历 nextExpirationTime 添加session
 - 启动线程
 
### 3. 设置请求处理器
1. 创建 FinalRequestProcessor 的实例 finalProcessor
2. 创建 SyncRequestProcessor 的实例 syncProcessor
3. 创建 PrepRequestProcessor 实例并赋值给 firstProcessor 
 