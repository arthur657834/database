
```
插件支持列表
https://www.elastic.co/guide/en/elasticsearch/reference/0.90/modules-plugins.html#analysis-plugins

bin/plugin install mobz/elasticsearch-head

bin/plugin install delete-by-query

1. 问题：ES的数据分布是什么样的？
答：数据分布是哈希分布，默认是对ID进行Hash取模，均衡分布在各个分片上。ID是UUID，Hash算法是MurMurHash3。
 
 
2. 问题：ES的Master节点为啥要奇数个？
答： 奇数方便票决，ES的master选举算法是,一半以上有资格成为Master的节点投票通过才能选举成功。剩下的节点无法单独构成集群，也能防止脑裂。
 
 
3. 问题：ES是否需要连接池？
答：不需要，ES是客户端负载均衡模式，内置了连接池。
 
 
4. 问题：ES的数据模型和存储模型分别是什么？
答：ES的数据模型是文档模型，存储模型是倒排索引
 
 
5. 问题：ES是Schema-less 还是 Schema-free？
答： ES是Schema-free，可以动态监测数据类型，自动给表建立表结构，动态增加字段。实际上还是有表结构的。
 
 
6. 问题：ES的复制协议是什么？
答：ES是基于主分片的复制协议（Primary-based protocol）
 
 
7.问题：ES的写操作会实时落盘吗？
答：不会实时落盘，当内存Buffer满的时候，或者触发Flush的时候。
 
 
8.问题：ES支持多表Join吗？
答：不支持，可以在建模阶段，使用父子表或者去规范化（Denormalization）设计。
```
