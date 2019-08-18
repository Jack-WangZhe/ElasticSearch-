## ElasticSearch简介及发展历史

### 一.Elastic从开源到上市

* Elastic Inc - 开源软件 / 上市公司
* 当前市值超过50亿美金，开盘当天涨幅高达94%
* ElasticSearch软件下载量，超过3.5亿次
* 10万+ 的社区成员
* 7200+ 订阅用户，分布在100+ 国家
* 云服务 - Elastic, Amazon, 阿里巴巴, 腾讯

### 二.ElasticSearch简介

#### 1.ElasticSearch - **开源分布式搜索分析引擎**

* 近实时（Near Real Time）
* 分布式存储、搜索、分析引擎

#### 2.Solr（Apache开源项目）

#### 3.Splunk（商业上市公司）

* Splunk是全球第一家上市的大数据公司

#### 4.ElasticSearch VS Solr

* 近些年ES逐渐上涨，Solr使用量逐渐下跌
* ElasticSearch和Solr均起源于Lucene
  * 基于Java语言开发的搜索引擎库类
  * 创建于1999年，2005年成为Apache顶级开源项目
  * Lucene具有高性能、易扩展的有点
  * Lucene的局限性
    * 只能基于Java语言开发
    * 类库的接口学习曲线陡峭
    * 原生并不支持水平扩展
* ElasticSearch诞生
  * 2004年Shay Banon基于Lucene开发了Compass
  * 2010年Shay Banon重写了Compass，取名ElasticSearch
    * 支持分布式，可水平扩展
    * 降低全文检索的学习曲线，可以被任何编程语言调用

#### 5.ElasticSearch分布式架构

* 集群规模可以从单个扩展至数百个节点
* 高可用&水平扩展
  * 服务和数据两个维度
* 支持不同的节点类型
  * 支持Hot&Warm架构（针对日志类的应用）

#### 6.ES支持多种方式集成接入

* 多种编程语言的类库（https://www.elastic.co/guide/en/elasticsearch/client/index.html）
  * 提供了API，可以使用Java/.NET/Python/Ruby/PHP/Groovy/Perl去访问ES
* Restful API（推荐使用） 和 Transport API
* 新版本的ES版本中还提供了JDBC&ODBC接入的方式

#### 7.ES的主要功能

* 海量数据的分布式存储以及集群管理
  * 服务与数据的高可用，水平扩展
* 近实时搜索，性能卓越
  * 结构化、全文、地理位置、自动完成
* 海量数据的近实时分析
  * 集合功能

#### 8.ES版本与升级情况

* 0.4:2010年2月第一次发布
* 1.0:2014年1月
* 2.0:2015年10月
* 5.0:2016年10月
* 6.0:2017年10月
* 7.0:2019年4月
* EOL Support - https://www.elastic.co/cn/support/eol

#### 9.ES版本升级变化

* 新特性5.X
  * Lucene 6.X 性能提升，默认打分机制从TF-IDF改为BM25
  * 支持Ingest节点、Painless Scripting、Completion suggested支持、原生的Java REST客户端
  * Type标记成deprecated，支持了Keyword的类型
  * 性能优化
    * 内部引擎溢出了避免同一文档并发更新的竞争锁，带来15%-20%的性能提升
    * Instant aggregation，支持分片上聚合的缓存
    * 新增了Profile API
* 新特性6.X
  * Lucene7.X
  * 新功能
    * 跨集群复制（CCR）
    * 索引生命周期管理
    * SQL的支持
  * 更友好的升级及数据迁移
    * 在主要版本之间的迁移更为简化，体验升级
    * 全新的基于操作的数据复制框架，可加快恢复数据
  * 性能优化
    * 有效存储稀疏字段的新方法，降低了存储成本
    * 在索引时进行排序，可加快排序的查询性能
* 新特性7.X
  * Lucene9.0
  * 重大改进-正式废除单个索引下多Type的支持
  * 7.1开始，Security功能免费使用
  * ECK-ElasticSearch Operator on Kubernetes
  * 新功能
    * New Cluster coordination
    * Feature - Complete High Level REST Client
    * Script Score Query
  * 性能优化
    * 默认的Primary Shared数从5改为1，避免Over Sharding
    * 性能优化，更快的Top K