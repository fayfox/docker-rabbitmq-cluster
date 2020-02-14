# 在docker中测试rabbitmq集群

配置了3个rabbitmq实例，分别为node1、node2、node3  
用haproxy和nginx分别做了负载均衡测试


### 启动容器

1、通过`docker-compose up -d`启动相关容器


2、分别进入node2，node3执行如下命令，加入集群

```shell
root@node2:/# rabbitmqctl stop_app
Stopping rabbit application on node rabbit@node2 ...
root@node2:/# rabbitmqctl reset
Resetting node rabbit@node2 ...
root@node2:/# rabbitmqctl join_cluster rabbit@node1
Clustering node rabbit@node2 with rabbit@node1
root@node2:/# rabbitmqctl start_app
Starting node rabbit@node2 ...
 completed with 4 plugins.
```

3、访问RabbitMQ Management管理后台

- node1节点的管理后台：http://localhost:15672/#/
- 基于Haproxy代理的管理后台：http://localhost:1081/#/
- 基于Nginx代理的管理后台：http://localhost:2081/#/

4、程序发布/接收消息端口

- 直连端口：5672、5673、5674
- 基于Haproxy负载均衡端口：1080
- 基于Nginx负载均衡端口：2080