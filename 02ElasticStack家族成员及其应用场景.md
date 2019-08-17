## ElasticStack家族成员及其应用场景

### 一.Elastic Stack生态圈

![](/Users/wangzhe/Practice/ElasticSearch核心入门与实战/ElasticSearch-Notes/图片集/02 Elastic Stack生态圈.png)

#### 1.Logstash：数据处理管道

* 开源的服务器端数据处理管道，支持从不同来源采集数据，转换数据，并将数据发送到不同的存储库中
* Logstash诞生于2009年，最初用来做日志的采集与处理
* Logstash创始人Jordan Sisel
* 2013年被ElasticSearch收购

#### 2.Logstash特性

* 实时解析和转换数据
  * 从IP地址破译除地理坐标
  * 将PII数据匿名化，完全排除敏感字段
* 可扩展
  * 200多个插件（日志、数据库、Arcsigh、Netflow）
* 可靠性安全性
  * Logstash会通过持久化队列来保证至少将运行中的事件送达一次
  * 数据传输加密
* 监控

#### 3.Kibana：可视化分析利器

* Kibana名字的含义 = Kiwifruit + Banana
* 数据可视化工具，帮助用户解开对数据的任何疑问
* 基于Logstash工具，2013年加入Elastic公司

#### 4.Elastic的发展

* 2015年3月收购Elastic Cloud，提供Cloud服务
* 2015年3月收购PacketBeat
* 2016年9月收购PreAlert - Machine Learning异常检测
* 2017年6月收购Opbeat进军APM
* 2017年11月收购Saas厂商Swiftype，提供网站和App搜索
* 2018年X-Pack开源



> 未完待续...