## ElasticSearch安装与配置

### 一.ElasticSearch安装

#### 1.安装Java

* ElasticSearch是基于Java开发的，故需先安装Java环境
* 从7.0开始ES内置了Java环境

#### 2.官网安装ES

| 目录    | 配置文件          | 描述                                           |
| ------- | ----------------- | ---------------------------------------------- |
| bin     |                   | 脚本文件，包括启动ES，安装插件。运行统计数据等 |
| config  | elasticsearch.yml | 集群配置文件，user，role based相关配置         |
| JDK     |                   | Java运行环境                                   |
| data    | path.data         | 数据文件                                       |
| lib     |                   | Java类库                                       |
| logs    | path.log          | 日志文件                                       |
| modules |                   | 包含所有ES模块                                 |
| plugins |                   | 包含所有已安装插件                             |

* <https://www.elastic.co/downloads/elasticsearch>下载压缩包，进入bin目录，执行elasticsearch命令即可启动ES

* 通过浏览器访问9200端口可以看到本地启动的ES的信息

  ```json
  {
      name: "Jack-2.local",
      cluster_name: "elasticsearch",
      cluster_uuid: "XEEHBEq8QhK7YhU5d0Ii7A",
      version: {
          number: "7.3.0",
          build_flavor: "default",
          build_type: "tar",
          build_hash: "de777fa",
          build_date: "2019-07-24T18:30:11.767338Z",
          build_snapshot: false,
          lucene_version: "8.1.0",
          minimum_wire_compatibility_version: "6.8.0",
          minimum_index_compatibility_version: "6.0.0-beta1"
      },
      tagline: "You Know, for Search"
  }
  ```

#### 3.JVM配置

* 修改JVM - config/jvm.options
  * 7.1下载的默认设置是1GB
* 配置的建议
  * 最小内存Xms和最大内存Xms设置成一样
  * Xms不要超过机器内存的50%
  * 不要超过30GB - https://www.elastic.co/blog/a-heap-of-trouble

#### 4.如何安装与查看插件

* 介绍链接：https://www.elastic.co/guide/en/elasticsearch/plugins/current/intro.html

* `bin/elasticsearch-plugin install 插件名如: analysis-icu(国际化分词插件)`安装插件
* `bin/elasticsearch-plugin list`查看本机安装了哪些插件
* 访问 localhost:9200/_cat/plugins 可以获得插件安装信息

### 二.运行多个ES实例

> ES的特色在于分布式，以下我们将用开发机举例，实现如何在一个开发机上运行多个ES实例

#### 1.如何在开发机上运行多个ES实例

* 实例代码:启动ES集群

  ```shell
  bin/elasticsearch -E node.name=node1 -E cluster.name=jackTest -E path.data=node1_data -d
  bin/elasticsearch -E node.name=node2 -E cluster.name=jackTest -E path.data=node2_data -d
  bin/elasticsearch -E node.name=node3 -E cluster.name=jackTest -E path.data=node3_data -d
  ```

  * node.name节点名称
  * cluster.name集群名称（相同集群名）
  * path.data为每个节点设置不同的存放数据的地址
  * -d表示后台运行

* 可以通过localhost:9200/_cat/nodes的方式查看节点

* 删除进程

  ```shell
  ps grep|elasticsearch / kill pid
  ```

  

