## Kibana的安装与界面浏览

### 一.Kibana的安装

#### 1.下载Kibana

* 下载地址<https://www.elastic.co/downloads/kibana>
* Kibana提供开箱即用的体验，解压缩即可使用
* 如果想定制化Kibana，可以通过修改kibana.yml文件完成

#### 2.启动Kibana

* 首先需要启动ES
* 再通过`bin/kibana`启动Kibana
* 通过访问`localhost:5601`访问Kibana
* Kibana提供了三个测试Sample data可以通过Add的方式进行添加，选择Add后，实际上就是将数据导入到了ES中，在Dashboard可以进行查看

#### 3.Kibana实用工具：Dev Tools

* 可以方便的在Kibana中执行ES的API
* 如在console中输入: `get /_cat/nodes?v`可以获取到ES中节点运行情况

#### 4.Kibana安装插件

* 可以通过 https://www.elastic.co/guide/en/kibana/current/known-plugins.html 查看官方文档

* 通过如下命令安装插件

  ```shell
  bin/kibana-plugin install plugin_location
  ```

* 通过如下命令查看插件列表

  ```shell
  bin/kibana-plugin list
  ```

* 通过如下命令移除Kibana

  ```shell
  bin/kibana remove
  ```

* Kibana可以通过插件增强应用，或增加图表展示的内容