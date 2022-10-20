 ES

1. es基础概念
   1. near realtime:近实时，新增/修改/删除后能查到需要1s（refresh interval）
   1. 集群cluster：一个或多个节点node,保存所有数据，提供联合索引和查询，集群默认名字为elasticsearch。节点node根据名字添加进对应集群
   1. 节点Node:a single server
   1. index：索引，有相似特点的文档的集合
   1. type: 索引index下的概念，粒度又小点
   1. ducument:文档，可被检索到的信息的基本单元，json格式文档
   1. shards&replicas:分片&副本
      1. 分片：横向扩展能力；给每个分片分配和并行化操作，提升性能，提高吞吐量。每个es分片是一个lucene index。单个索引最多存2147483519（Integer.MAX_VALUE-128）个文档。
      1. 副本：高可用，故障恢复（副本replicas与primary放在不同node上）。**`扩大搜索的吞吐量`**（意思是 每个副本都查询，然后在汇合？），在副本上并发执行搜索

2. 集群监控&命令行操作

   1. 看集群健康：curl -X GET -u undefined:$ESPASS "localhost:9200/_cat/health?v&pretty"；v显示列名

   2. 看集群节点：curl -X GET -u undefined:$ESPASS "localhost:9200/_cat/nodes?v&pretty"

   3. 建customer index : curl -X PUT -u undefined:$ESPASS "localhost:9200/customer?pretty";pretty让返回格式化

   4. 查看所有索引index :  curl -X GET -u undefined:$ESPASS "localhost:9200/_cat/indices?v&pretty"

   5. 把id=1的文档放入索引customer下的external type下,相同id会覆盖(整个文档覆盖)，否则新增。不加会默认设置一个id：

      1. curl -X PUT -u undefined:$ESPASS "localhost:9200/customer/external/1?pretty" -H 'Content-Type: application/json' -d'
         {
           "name": "John Doe"
         }
         '

   6. 查看id=1的文档：curl -X GET -u undefined:$ESPASS "localhost:9200/customer/external/1?pretty"

   7. 删除索引index=customer: curl -X DELETE -u undefined:$ESPASS "localhost:9200/customer?pretty"

   8. 格式：<REST Verb> /<Index>/<Type>/<ID>

   9. 不加id的新增用POST：curl -X POST "localhost:9200/customer/external?pretty" -d '{"name":"jane Doee"}'

   10. 更新文档`字段`__update：curl -X POST "localhost:9200/customer/external/1/_update?pretty" -d '{"doc" : {"name":"gogo", "age":30}}' 

   11. 删除文档 ： curl -X DELETE -u undefined:$ESPASS "localhost:9200/customer/external/2?pretty&pretty"

   12. 批量新增或覆盖 ：_bulk

       ```
       curl -X POST -u undefined:$ESPASS "localhost:9200/customer/external/_bulk?pretty&pretty" -H 'Content-Type: application/json' -d'
       {"index":{"_id":"1"}}
       {"name": "John Doe" }
       {"index":{"_id":"2"}}
       {"name": "Jane Doe" }
       '
       ```

   13. 批量更新或删除：

       curl -X POST -u undefined:$ESPASS "localhost:9200/customer/external/_bulk?pretty&pretty" -H 'Content-Type: application/json' -d'
       {"update":{"_id":"1"}}
       {"doc": { "name": "John Doe becomes Jane Doe" } }
       {"delete":{"_id":"2"}}
       '
       
   13. 批量导入数据：curl -H "Content-Type: application/json" -XPOST 'localhost:9200/bank/account/_bulk?pretty&refresh' --data-binary "@accounts.json"

       [链接](https://www.csdn.net/tags/MtTaYg2sMDk1OTctYmxvZwO0O0OO0O0O.html)json格式，index,data
       
   13. 查询数据：

       1. curl -X GET -u undefined:$ESPASS "localhost:9200/bank/_search?q=*&sort=account_number:asc&pretty&pretty"
       2. curl -X GET -u undefined:$ESPASS "localhost:9200/bank/_search?pretty" -H 'Content-Type: application/json' -d'
          {
            "query": { "match_all": {} },
            "sort": [
              { "account_number": "asc" }
            ]
          }
          '
       3. 查部分字段_source：curl -X GET -u undefined:$ESPASS "localhost:9200/logstash/_search?pretty" -H 'Content-Type: application/json' -d'
          {
            "query": { "match_all": {} },
            "_source": ["size"]
          }
          '
       
     16. 查询语句
   
         
   
   ```
   查number是20的书记
   GET /bank/_search
   {
     "query": { "match": { "account_number": 20 } }
   }
   
   查address包含mill的文档
   GET /bank/_search
   {
     "query": { "match": { "address": "mill" } }
   }
   
   查address包含mill或lane的文档。会客户端分词
   GET /bank/_search
   {
     "query": { "match": { "address": "mill lane" } }
   }
   
   查包含mill lane的文档
   GET /bank/_search
   {
     "query": { "match_phrase": { "address": "mill lane" } }
   }
   
   
   查包含mill和lane的文档
   GET /bank/_search
   {
     "query": {
       "bool": {
         "must": [
           { "match": { "address": "mill" } },
           { "match": { "address": "lane" } }
         ]
       }
     }
   }
   
   查address包含mill或lane的文档
   GET /bank/_search
   {
     "query": {
       "bool": {
         "should": [
           { "match": { "address": "mill" } },
           { "match": { "address": "lane" } }
         ]
       }
     }
   }
   
   查不包含mill和lane的文档
   GET /bank/_search
   {
     "query": {
       "bool": {
         "must_not": [
           { "match": { "address": "mill" } },
           { "match": { "address": "lane" } }
         ]
       }
     }
   }
   
   查age=40且state!=ID的文档
   GET /bank/_search
   {
     "query": {
       "bool": {
         "must": [
           { "match": { "age": "40" } }
         ],
         "must_not": [
           { "match": { "state": "ID" } }
         ]
       }
     }
   }
   
   查范围数据。
   GET /bank/_search
   {
     "query": {
       "bool": {
         "must": { "match_all": {} },
         "filter": {
           "range": {
             "balance": {
               "gte": 20000,
               "lte": 30000
             }
           }
         }
       }
     }
   }
   ```
   
   ​    查询结果中 文档的_score表示和search query的关联度，值越大关联度越强。有filter的查询不计算这个值，因为已经有了限定也是为了提升性能。
   
   
   
   ```
   聚合查询
   GET /bank/_search
   {
     "size": 0,   #表示不需要hits数据，只要aggregations聚合数据
     "aggs": {
       "group_by_state": {
         "terms": {
           "field": "state.keyword"
         }
       }
     }
   }
   
   类似sql:SELECT state, COUNT(*) FROM bank GROUP BY state ORDER BY COUNT(*) DESC
   
   ```
   
   
   
   3. 数据复制模型&写模型&读模型
      1. 数据复制模型：主备份模型，分片主节点primary负责接收验证、处理增删改操作，处理完了在发送给多个副本replicas节点并行处理，
      2. 写数据：写请求路由到对应分片的主节点primary，主节点验证后执行，执行完了同步请求到该主节点的in-sync副本集合，多个副本节点并行处理完后，主节点收到ack给客户端返回成功信息。最慢的副本成为短板。（产生很多问题？磁盘崩溃/节点连不上/配置问题导致副本执行失败，没有副本？）
      3. 读数据：读请求到任意节点A，节点把请求路由到对应分片（一个或多个），每个分片可能包含数据的子集。从分片复制群组（replication group）,采用round robin负载均衡到某个主节点或副本节点。A节点发送分片级别的读请求到该分片节点。A节点汇合整理返回的数据，并发送给客户端。

[参考](https://www.elastic.co/guide/en/elasticsearch/reference/5.3/gs-basic-concepts.html#getting-started-shards-and-replicas)

1)https://www.elastic.co/guide/en/elasticsearch/reference/5.3/gs-basic-concepts.html#getting-started-shards-and-replicas

