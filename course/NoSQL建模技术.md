# NoSQL建模技术

- 键值存储数据库:Oracle Coherence,Redis,Kyoto Cabinet
- Big Table存储数据库:Apache HBase,Apache Cassandra
- 文档数据库:MongoDB,CouchDB
- 全文搜索引擎:Apache Lucene,Apache Solr,ES
- 图形数据库:Neo4j,FlockDB

+ [概念技术](#概念技术) 
+ [一般建模技术](#一般建模技术)
+ [主流NoSQL介绍及适用场景](#主流NoSQL介绍及适用场景)
  
## 概念技术

- 去规范化(Denormalization)
  - 适用性:键值存储数据库,文档数据库,Big Table存储数据库
  
- 聚合(Aggregates)
  - 适用性:键值存储数据库,文档数据库,Big Table存储数据库
  
- 应用端连接(Application Side Joins)
  - 适用性:键值存储数据库,文档数据库,Big Table存储数据库,图形数据库
  
## 一般建模技术

- 原子聚合(Atomic Aggregates)
  - 适用性:键值存储,文档数据库,BigTable风格的数据库
- 可枚举主键(Enumerable Keys)
  - 适用性:键值存储
- 降维(Dimensionality Reduction)
  - 适用性:键值存储,文档数据库,BigTable风格的数据库
- 索引表(Index Table)
  - 适用性:BigTable风格的数据库
- 组合主键索引(Composite Key Index)
  - 适用性:BigTable风格的数据库
- 组合主键的聚合
  - 适用性:有序键值存储,BigTable风格的数据库
- 倒排搜索-直接聚合
  - 适用性:键值存储,BigTable风格的数据库,文档数据库
- 树聚合(Tree Aggregation)
  - 适用性:键值存储,文档数据库
- 邻接列表(Adjacency Lists)
  - 适用性:键值存储,文档数据库
- 物化路径
  - 适用性:键值存储,文档数据库,搜索引擎
- 嵌套集合(Nested Sets)
  - 适用性:键值存储,文档数据库
- 扁平化嵌套文件：字段名称编号
  - 适用性:搜索引擎
- 扁平化嵌套文件：近似查询
  - 适用性:搜索引擎
- 批量图处理
  - 适用性:键值存储,文档数据库,BigTable风格的数据库
  
## 主流NoSQL介绍及适用场景

- Redis
  - 适用场景
  
  	- 数据变化较少，执行预定义查询，进行数据统计的应用程序
  	- 需要提供数据版本支持的应用程序
    - 例如：股票价格、数据分析、实时数据搜集、实时通讯、分布式缓存
    
- MongoDB
  - 适用场景
  
  	- 需要动态查询支持
  	- 需要使用索引而不是map/reduce功能
  	- 需要对大数据库有性能要求
    - 需要使用CouchDB但因为数据改变太频繁而占满内存
  
- Neo4j
  - 适用场景
  
  	- 适用于图形一类数据
  	- 这是 Neo4j与其他NoSQL数据库的最显著区别
    - 例如：社会关系，公共交通网络，地图及网络拓谱
    
- Cassandra
  - 适用场景
  
  	- 银行业，金融业
    - 写比读更快
    
- HBase
  - 适用场景
  
  	- 对大数据进行随机、实时访问的场合
    - 例如： Facebook消息数据库
    
- CouchDB
  - 适用场景
  
  	- 数据变化较少，执行预定义查询，进行数据统计的应用程序
  	- 需要提供数据版本支持的应用程序。
    - 例如： CRM、CMS系统。 master-master复制对于多站点部署是非常有用的。
    
- ES/Solr
  - 适用场景
  
    - 外置搜索引擎
    - 日志分析