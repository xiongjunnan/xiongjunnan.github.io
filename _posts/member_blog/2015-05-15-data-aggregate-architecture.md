---
layout:     post
title:      【微主题延伸】聚集第三方数据展示系统架构如何设计
category: member_blog
description: 如果某旅游网想把旅游信息展示到第三方平台上或者说某系统只是把好多其他商家的数据聚合到统一的系统上，一般如何架构？
---
此文根据【QCon高可用架构群】分享内容，由群内成员个人整理，转发请注明出处。

 > 引子： 如果某旅游网想把旅游信息展示到第三方平台上或者说某系统只是把好多其他商家的数据聚合到统一的系统上，一般如何架构？
 
 
## 数据对接方式选型，PULL 还是 POST？
  
#####1、如果平台系统很大部分是通过聚合第三方数据再展示

<strong>推荐方式：</strong>  
第三方post数据，自己做统一数据开放API。

<strong>优势：</strong>  
1、一次完成，无限制接入商户，只要提高聚合平台的服务能力   
2、实时性高、数据交互少

<strong>存在问题和约束：</strong>   
1、由于第三方服务的可靠性和误操作等无法保障，所以对自身服务的稳定性要求高。  
2、数据更新的时效性由第三方控制（当然平台服务本身也可控制）  
3、平台方的需要支撑的服务能力，只能预估，不好控制，比如第三方数据量突然暴增


#####2、如果接入的第三方平台的数据和数量有限

<strong>推荐方式：</strong>
平台方pull  

<strong>优势：</strong>  
服务能力和平台稳定性只和自己有关，不依赖第三方服务

<strong>存在问题和约束：</strong>  
此类方式需根据第三方的API，把所有的数据转换成自己格式，每接入一家第三方需要增加研发工作量。
 

## 系统架构

###应用划分
按业务划分成子模块、服务或子系统

###高性能
1、首先平台接入，数据存储和读取等方面需要隔离和切分 
  
2、平台接入使用使用MQ提高吞吐  
可选择：自建简易Q，Redis、Kafka，Rocketmq、Rabbitmq、beanstalkd、NSQ等等。  
 
3、读取数据使用Cache    
可选择：Redis、Memcache、EhCache、JBoss Cache等等。 

###可用性
集群、负载均衡   

软件：括nginx、LVS、haproxy等  
硬件：NetScaler、F5、Radware等

###日志
日志收集可选择：
Flume、Kafka、Scribe、Chukwa等

###存储

可选择：mysql、hbase、Mongodb、Hypertable、CouchBase、Cassandra等等

###数据处理和分析
可选择：JStorm、Storm、hadoop、Drill、Samza、Spark等


总原则：系统是从小到大慢慢演变的，架构是长出来的，架构因业务而变。所以选择的时候除了考虑约束之外，也需考虑成本，以及相应的可扩展性.






 

