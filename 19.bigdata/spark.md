### 1. spark简介

- Spark 作为新的分布式数据处理引擎，对 MapReduce 进行了很多改进，使得性能大大提升，并且更加适用于新时代的数据处理场景。但是，Spark 并不是一个完全替代 Hadoop 的全新工具。

  - 因为 Hadoop 还包含了很多组件：
    - 数据存储层：分布式文件存储系统 HDFS，分布式数据库存储的 HBase；
    - 数据处理层：进行数据处理的 MapReduce，负责集群和资源管理的 YARN；
    - 数据访问层：Hive、Pig、Mahout……

  - 从狭义上来看，Spark 只是 MapReduce 的替代方案，大部分应用场景中，它还要依赖于 HDFS 和 HBase 来存储数据，依赖于 YARN 来管理集群和资源。
  - 此外，作为通用的数据处理平台，Spark 有五个主要的扩展库，分别是支持结构化数据的 Spark SQL、处理实时数据的 Spark Streaming、用于机器学习的 MLlib、用于图计算的 GraphX、用于统计分析的 SparkR。这些扩展库与 Spark 核心 API 高度整合在一起，使得 Spark 平台可以广泛地应用在不同数据处理场景中。