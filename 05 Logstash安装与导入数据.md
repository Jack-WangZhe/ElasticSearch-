## Logstash安装与导入数据

> 下载最 MovieLens 最小测试数据集：<https://grouplens.org/datasets/movielens/>
>
> Logstash 下载：<https://www.elastic.co/cn/downloads/logstash>
>
> Logstash 参考文档：<https://www.elastic.co/guide/en/logstash/current/index.html>

### 一.Logstash的安装

#### 1.安装流程

* 到官网下载压缩包并解压
* 准备logstash.conf配置文件，执行`bin/logstash -f logstash.conf`启动

#### 2.使用实例

* 在grouplens下载数据集

* 实例logstash.conf文件内容

  ```yaml
  input {
    file {
      path => "实际的movies.csv路径:movies.csv"
      start_position => "beginning"
      sincedb_path => "/dev/null"
    }
  }
  
  # 对CSV进行处理部分
  filter {
    csv {
      separator => ","
      columns => ["id","content","genre"]
    }
  
    mutate {
      split => { "genre" => "|" }
      remove_field => ["path", "host","@timestamp","message"]
    }
  
    mutate {
  
      split => ["content", "("]
      add_field => { "title" => "%{[content][0]}"}
      add_field => { "year" => "%{[content][1]}"}
    }
  
    mutate {
      convert => {
        "year" => "integer"
      }
      strip => ["title"]
      remove_field => ["path", "host","@timestamp","message","content"]
    }
  }
  output {
     elasticsearch {
     	 # 将结果输出到ES中
       hosts => "http://localhost:9200"
       index => "movies"
       document_id => "%{id}"
     }
    stdout {}
  }
  ```

* 执行`sudo ./logstash -f logstash.conf`启动Logstash

* 启动后可以在控制台中看到大量数据在写入ES中

