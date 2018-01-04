## javaWeb架构师必备
  + 高可用
  	- 负载均衡（负载均衡算法）
  	- 反向代理
  	- 服务隔离
  	- 服务限流
  	- 服务降级（自动优雅降级）
  	- 失效转移
  	- 超时重试（代理超时、容器超时、前端超时、中间件超时、数据库超时、NoSql超时）
    - 回滚机制（上线回滚、数据库版本回滚、事务回滚）
  + 高并发
  	- 应用缓存
  	- HTTP 缓存
  	- 多级缓存
  	- 分布式缓存
  	- 连接池
    - 异步并发
  + 分布式事务
  	- 二阶段提交(强一致)
  	- 三阶段提交(强一致)
    - 消息中间件(最终一致性)，推荐阿里的 RocketMQ。
    
    ![分布式事务](./resource/分布式事务.png)
    
  + 队列
  	- 任务队列
  	- 消息队列
    - 请求队列
  + 扩容
  	- 单体垂直扩容
  	- 单体水平扩容
  	- 应用拆分
  	- 数据库拆分
  	- 数据库分库分表
  	- 数据异构
    - 分布式任务
  + 网络安全
  	- SQL 注入
  	- XSS 攻击
  	- CSRF 攻击
    - 拒绝服务（DoS，Denial　of　Service）攻击
  
## javaWeb架构工具
  + 操作系统
  
  Linux（必备）、某软的
  
  + 负载均衡
  
  DNS、F5、LVS、Nginx、OpenResty、HAproxy、负载均衡SLB（阿里云）
  
  + 分布式框架
  
  Dubbo、Motan、Spring-Could
  
  + 数据库中间件
  
  DRDS （阿里云）、Mycat、360 Atlas、Cobar (不维护了)
  
  + 消息队列
  
  RabbitMQ、ZeroMQ、Redis、ActiveMQ、Kafka
  
  + 注册中心
  
  Zookeeper、Redis
  
  + 缓存
  
  Redis、Oscache、Memcache、Ehcache
  
  + 集成部署
  
  Docker、Jenkins、Git、Maven
  
  + 存储
  
  OSS、NFS、FastDFS、MogileFS
  
  + 数据库
  
  MySQL、Redis、MongoDB、PostgreSQL、Memcache、HBase
  
  + 网络
  
  专用网络 VPC、弹性公网 IP、CDN