## ElasticSearch基本概念

### 一.文档（Document）

#### 1.ElasticSearch是面向文档的，文档是所有可搜索数据的最小单位

* 日志文件中的日志项
* 一本电影的具体信息 、 一张唱片的详细信息
* MP3播放器里的一首歌 、 一篇PDF文档中的具体内容

#### 2.文档会被序列化成JSON格式，保存在ElasticSearch中

* JSON对象由字段组成
* 每个字段都有对应的字段类型（字符串、数值、布尔、日期、二进制、范围类型）

#### 3.每个文档都有一个Unique ID

* 你可以自己指定ID
* 或者通过ES自动生成

#### 4.JSON文档

* 一篇文档包含了一系列的字段。类似数据库表中的一条记录。

* JSON文档，格式灵活，不需要预先定义格式

  * 字段的类型可以指定或者通过ElasticSearch自动推算
  * 支持数组、支持嵌套

* 如会将CSV文件的内容转换成如下的格式

  ```json
  {
      "year": 1997,
      "@version": "1",
      "genre": [
          "Children","Fantasy","Comedy"
      ],
      "id": "1",
      "title": "Toy Story"
  }
  ...
  ```

#### 5.文档的元数据

* 每一篇文档都有对应的元数据

* 元数据实例

  ```json
  {
      "_index": "movies",
      "_type": "_doc",
      "_id": "1",
      "_score": 14.69302,
      "_source": {
          "year": 1997,
          "@version": "1",
          "genre": [
              "Children","Fantasy","Comedy"
          ],
          "id": "1",
          "title": "Toy Story"
      }
  },
  ...
  ```

* 元数据，用于标注文档的相关信息

  * _index: 文档所属的索引名
  * _type: 文档所属的类型名
  * _id: 文档唯一ID
  * _source: 文档的原始JSON数据
  * _all: 整合所有字段内容到该字段，7.0版本已被废除
  * _version: 文档的版本信息
  * _score: 相关性打分

### 二.索引

#### 1.索引实例

```json
{
    "movies": {
        "settings": {
            "index": {
                "creation_date": "1552737458543"，
                "number_of_shards": "2",
                "number_of_replicas": "0",
                "uuid": "Qnd7scnskscai8sdahda8",
                "version": {
                	"created": "6060299"
            	},
            	"provided_name": "movies"
            }
        }
    }
}
```

#### 2.Index - 索引是文档的容器，是一类相似文档的集合

* index体现了逻辑空间的概念：每个索引都有自己的Mapping定义文件，用于定义包含的文档的字段名和字段类型
* Shard体现了物理空间的概念：索引中的数据分散在Shard上

* 索引的Mapping与Settings
  * Mapping定义文档字段的类型
  * Setting定义要用多少分片，数据是怎样分布的

#### 3.索引的不同语意

- 名词： 一个ElasticSearch集群中可以创建很多个不同的索引
- 动词： 保存一个文档到ElasticSearch的过程页脚索引（indexing）
  - ES中，创建一个倒排索引的过程
- 名词： 一个B树索引，一个倒排索引

#### 4.Type

* 在7.0之前，一个index可以设置多个Types
* 6.0开始，Type已经被Deprecated；7.0开始，一个索引只能创建一个Type - "_doc"

### 三.关系型数据库与ES抽象与类比

#### 1.传统关系型数据库和ElasticSearch的区别

* ElasticSearch - 偏向 Schemaless / 相关性 / 高性能全文检索
* RDMS - 偏向 事务性 / Join

#### 2.类比关系表

| RDBMS  | ElasticSearch |
| ------ | ------------- |
| Table  | Index(Type)   |
| Row    | Document      |
| Column | Filed         |
| Schema | Mapping       |
| SQL    | DSL           |

### 四.ES RestAPI集成

#### 1.调用流程

* ES提供RestAPI供其他程序调用，从而实现应用与ES的集成
* Client Application 发送 HTTP Request 到ES上，ES给出HTTP Response返回给Client Application

#### 2.结合Kibana演示

* 选中Kibana左侧选项中最后一项可以选择索引管理进行索引的查看与管理操作
* 选中Kibana左侧选项中开发工具项通过Console可以发送RestAPI请求到ES中获得相应数据