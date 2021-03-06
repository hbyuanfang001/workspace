## javaWeb网站架构演进

- 初始搭建
  
  ![初始搭建](./resource/初始搭建.png)
  最开始，就是各种框架一搭，然后扔到 Tomcat 容器中跑，这时候我们的文件、数据库、应用都在一个服务器上。

- 服务分离

  ![服务分离](./resource/服务分离.png)
  由于我们是单体架构，优化架构在短时间内是不现实的，增加机器是一个不错的选择。这时，我们可能要把应用和数据库服务单独部署，如果有条件也可以把文件服务器单独部署。
  
- 反向代理

  ![反向代理](./resource/反向代理.png)
  为了提升服务处理能力，我们在 Tomcat 容器前加一个代理服务器，一般使用 Nginx，当然你如果更熟悉 Apache 也未尝不可。
  
  用户的请求发送给反向代理，然后反向代理把请求转发到后端的服务器。
  
  从严格意义上说，Nginx 是属于 Web 服务器，一般处理静态 HTML、CSS、JS 请求；而 Tomcat 属于 Web 容器，专门处理 JSP 请求，当然 Tomcat 也是支持 Html 的，只是效果没 Nginx 好而已。

  - 反向代理的优势，如下所示：
	- 隐藏真实后端服务。
	- 负载均衡集群。
	- 高可用集群。
	- 缓存静态内容实现动静分离。
	- 安全限流。
	- 静态文件压缩。
	- 解决多个服务跨域问题。
	- 合并静态请求(HTTP/2.0后已经被弱化)。
	- 防火墙。
    - SSL 以及 http2。
    
- 动静分离

  ![动静分离](./resource/动静分离.png)
  基于以上 Nginx 反向代理，我们还可以实现动静分离，静态请求如 HTML、CSS、JS 等请求交给 Nginx 处理，动态请求分发给后端 Tomcat 处理。
  
  Nginx 升级到 1.9.5+ 可以开启 HTTP/2.0 时代，加速网站访问。当然，如果公司不差钱，CDN 也是一个不错的选择。

- 服务拆分
  - Dubbo
  
  ![Dubbo](./resource/Dubbo.png)
  
  - SpringCloud
  
  	- 服务发现——Netflix Eureka
  	- 客服端负载均衡——Netflix Ribbon
  	- 断路器——Netflix Hystrix
  	- 服务网关——Netflix Zuul
    - 分布式配置——Spring Cloud Config
    
  - 微服务与轻量级通讯
  
    - 同步通信和异步通信
    - 远程调用 RPC
    - REST
    - 消息队列
    
- 持续集成

  你可能会用到以下工具：Docker、Jenkins、Git、Maven
  
  基本拓扑结构如下所示：
  
  ![持续集成拓扑结构](./resource/持续集成拓扑结构.png)
  
  整个持续集成平台的架构演进，如下图所示：
  
  ![持续集成平台架构演进](./resource/持续集成平台架构演进.png)
  
- 服务集群
  - Linux集群
    - 高可用集群
    - 负载均衡集群
    - 科学计算机群
  
  ![负载均衡集群](./resource/负载均衡集群.png)
  
  - 负载均衡实现
  
    - 负载均衡实现的三种方法：
    
      - DNS 负载均衡，一般域名注册商的 DNS 服务器不支持，但我用的阿里云解析已经支持。
      - 四层负载均衡(F5、LVS)，工作在 TCP 协议下。
      - 七层负载均衡(Nginx、haproxy)，工作在 HTTP 协议下。
      
  - 分布式Session
  
  大家都知道，服务一般分为有状态和无状态，而分布式 Session 就是针对有状态的服务。
  
  - 分布式 Session 的几种实现方式：
  	- 基于数据库的 Session 共享。
  	- 基于 resin/tomcat web 容器本身的 Session 复制机制。
  	- 基于 oscache/Redis/memcached 进行 Session 共享。
  	- 基于 cookie 进行 Session 共享。
  - 分布式 Session 的几种管理方式：
	- Session Replication 方式管理 (即 Session 复制)。
	  - 简介：将一台机器上的 Session 数据广播复制到集群中其余机器上。
	  - 使用场景：机器较少，网络流量较小。
	  - 优点：实现简单、配置较少、当网络中有机器 Down 掉时不影响用户访问。
	  - 缺点：广播式复制到其余机器有一定延时，带来一定网络开销。
	- Session Sticky 方式管理。
	  - 简介：即粘性 Session、当用户访问集群中某台机器后，强制指定后续所有请求均落到此机器上。
	  - 使用场景：机器数适中、对稳定性要求不是非常苛刻。
	  - 优点：实现简单、配置方便、没有额外网络开销。
	  - 缺点：网络中有机器 Down 掉时，用户 Session 会丢失、容易造成单点故障。
	- 缓存集中式管理。
	  - 简介：将 Session 存入分布式缓存集群中的某台机器上，当用户访问不同节点时先从缓存中拿 Session 信息。
	  - 使用场景：集群中机器数多、网络环境复杂。
	  - 优点：可靠性好。
      - 缺点：实现复杂，稳定性依赖于缓存的稳定性、Session 信息放入缓存时要有合理的策略写入。
      
    -目前生产中使用到的：
      - 基于 Tomcat 配置实现的 Mem Cache 缓存管理 Session 实现(麻烦)。
      - 基于 Os Cache 和 shiro 组播的方式实现(网络影响)。
      - 基于 Spring-Session+Redis 的方式实现(最适合)。
      
  - 负载均衡策略
  
  负载均衡策略的优劣及其实现的难易程度有两个关键因素：负载均衡算法，对网络系统状况的检测方式和能力。
  
    - rr 轮询调度算法
    
    顾名思义，轮询分发请求。优点是实现简单，缺点是不考虑每台服务器的处理能力。
    
    - wrr 加权调度算法
    
    我们给每个服务器设置权值 weight，负载均衡调度器根据权值调度服务器，服务器被调用的次数跟权值成正比。优点是考虑了服务器处理能力的不同。
    
    - sh 原地址散列
    
    提取用户 IP，根据散列函数得出一个 key，再根据静态映射表，查出对应的 value，即目标服务器 IP。一单目标机器超负荷，则返回空。
    
    - dh 目标地址散列
    
    同上，只是现在提取的是目标地址的 IP 来做哈希。优点是以上两种算法都能实现同一个用户访问同一个服务器。
    
    - lc 最少连接
    
    优先把请求转发给连接数少的服务器。优点是使得集群中各个服务器的负载更加均匀。
    
    - wlc 加权最少连接
    
    在 lc 的基础上，为每台服务器加上权值。算法为：（活动连接数*256+非活动连接数）÷权重 ，计算出来的值小的服务器优先被选择。优点是可以根据服务器的能力分配请求
    
    - sed 最短期望延迟
    
    sed 跟 wlc 类似，区别是不考虑非活动连接数。算法为：（活动连接数+1)*256÷权重，同样计算出来的值小的服务器优先被选择
    
    - nq 永不排队
    
    改进的 sed 算法，我们想一下什么情况下才能“永不排队”，那就是服务器的连接数为 0 的时候，那么假如有服务器连接数为 0，均衡器直接把请求转发给它，无需经过 sed 的计算
    
    - LBLC 基于局部性的最少连接
    
    均衡器根据请求的目的 IP 地址，找出该 IP 地址最近被使用的服务器，把请求转发之，若该服务器超载，则采用最少连接数算法
    
    - LBLCR 带复制的基于局部性的最少连接
    
    均衡器根据请求的目的 IP 地址，找出该 IP 地址最近使用的“服务器组”，注意，这里不是具体某个服务器，然后采用最少连接数算法，从该组中挑出具体的某台服务器出来，把请求转发之。
    
    若该服务器超载，那么根据最少连接数算法，从在集群的非本服务器组的服务器中，找出一台服务器出来，加入本服务器组，然后把请求转发之
    
- 读写分离

  MySQL 主从配置，读写分离并引入中间件，开源的 MyCat，阿里的 DRDS 都是不错的选择
  
  如果是对高可用要求比较高，但是又没有相应的技术保障，建议使用阿里云的 RDS 或者 Redis 相关数据库，省事省力又省钱
  
- 全文检索

  如果有搜索业务需求，引入 solr 或者 elasticsearch 也是一个不错的选择，不要什么都塞进关系型数据库
  
- 缓存优化

  引入缓存无非是为了减轻后端数据库服务的压力，防止其"罢工"。
  
  常见的缓存服务有：Ehcache、OsCache、MemCache、Redis，它们都是主流经得起考验的缓存技术实现，特别是 Redis 已大规模运用于分布式集群服务中，并证明了自己优越的性能
  
- 消息队列

  - 异步通知
  
  比如短信验证，邮件验证这些非实时反馈性的逻辑操作
  
  ![异步通知](./resource/异步通知.png)
  
  - 流量削锋
  
  应该是消息队列中的常用场景，一般在秒杀或团抢活动中使用广泛
  
  - 日志处理
  
  系统中的日志是必不可少的，但是如何去处理高并发下的日志却是一个技术活，一不小心可能会压垮整个服务
  
  工作中我们常用到的开源日志 ELK，为嘛中间会加一个 Kafka 或者 Redis 就是这么一个道理(一群人涌入和排队进的区别)
  
  - 消息通讯
  
  点对点通信(个人对个人)或发布订阅模式(聊天室)
  
- 日志服务

  消息队列中提到的 ELK 开源日志组件对于中小型创业公司是一个不错的选择
  
  ![日志服务](./resource/日志服务.png)
  
- 安全优化

  以上种种，没有安全做保证，一切都会归于零：
  - 阿里云的 VPN 虚拟专有网络以及安全组配置。
  - 自建机房的话，要自行配置防火墙安全策略。
  - 相关服务访问，比如 MySQL、Redis、Solr 等如果没有特殊需求尽量使用内网访问并设置鉴权。
  - 尽量使用代理服务器，不要对外开放过多的端口。
  - HTTPS 配合 HTTP/2.0 也是个不错的选择。