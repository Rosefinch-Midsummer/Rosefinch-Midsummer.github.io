---
title: "Docker命令指北"
date: 2025-06-22T22:34:25+08:00
lastmod: 2025-06-22T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- Docker
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
---


# 前言

每年都学Docker，我都对自己有点无语了~

这次应该算是学好了，后续应该会接着看K8s和podman相关的内容。

相关链接：

[Runoob-Docker](https://www.runoob.com/docker/docker-tutorial.html)
# Docker 资源汇总

---

### Docker 资源

- Docker 官方主页: [https://www.docker.com](https://www.docker.com/)
- Docker 官方博客: [https://blog.docker.com/](https://blog.docker.com/)
- Docker 官方文档: [https://docs.docker.com/](https://docs.docker.com/)
- Docker Store: [https://store.docker.com](https://store.docker.com/)
- Docker Cloud: [https://cloud.docker.com](https://cloud.docker.com/)
- Docker Hub: [https://hub.docker.com](https://hub.docker.com/)
- Docker 的源代码仓库: [https://github.com/moby/moby](https://github.com/moby/moby)
- Docker 发布版本历史: [https://docs.docker.com/release-notes/](https://docs.docker.com/release-notes/)
- Docker 常见问题: [https://docs.docker.com/engine/faq/](https://docs.docker.com/engine/faq/)
- Docker 远端应用 API: [https://docs.docker.com/develop/sdk/](https://docs.docker.com/develop/sdk/)

### Docker 国内镜像

阿里云的加速器：[https://help.aliyun.com/document_detail/60750.html](https://help.aliyun.com/document_detail/60750.html)

网易加速器：http://hub-mirror.c.163.com

官方中国加速器：https://registry.docker-cn.com

ustc 的镜像：https://docker.mirrors.ustc.edu.cn

daocloud：https://www.daocloud.io/mirror#accelerator-doc（注册后使用）



# Docker简介

![](https://www.runoob.com/wp-content/uploads/2016/04/docker01.png)

Docker 是一个开源的应用容器引擎，基于 Go 语言并遵从 Apache2.0 协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

Docker 从 17.03 版本之后分为 CE（Community Edition: 社区版） 和 EE（Enterprise Edition: 企业版），我们用社区版就可以了。

谁适合阅读本教程？

本教程适合运维工程师及后端开发人员，通过本教程你可以一步一步了解 Docker 的使用。

---

阅读本教程前，您需要了解的知识

在阅读本教程前，你需要掌握 Linux 的常用命令。你可以通过本站的 [Linux 教程](https://www.runoob.com/linux/linux-tutorial.html) 来学习相关命令。

---

Docker 的应用场景：

- **微服务架构：** 每个服务独立容器化，便于管理和扩展。
- **CI/CD流水线：** 与 Jenkins/GitLab CI 集成，实现自动化构建和测试。
- **开发环境标准化：** 新成员一键启动全套依赖服务（如数据库、消息队列）。
- **云原生基础：** Kubernetes 等编排工具基于 Docker 管理容器集群。

---

核心优势：

- **跨平台一致性：** 解决"在我机器上能跑"的问题，确保开发、测试、生产环境一致。
- **资源高效：** 容器直接共享主机内核，无需虚拟化整个操作系统，节省内存和 CPU。
- **快速部署：** 秒级启动容器，支持自动化扩缩容。
- **隔离性：** 每个容器拥有独立的文件系统、网络和进程空间。

---

核心概念：

- **容器（Container）：** 轻量化的运行实例，包含应用代码、运行时环境和依赖库。基于镜像创建，与其他容器隔离，共享主机操作系统内核（比虚拟机更高效）。
- **镜像（Image）：** 只读模板，定义了容器的运行环境（如操作系统、软件配置等）。通过分层存储（Layer）优化空间和构建速度。
- **Dockerfile：** 文本文件，描述如何自动构建镜像（例如指定基础镜像、安装软件、复制文件等）。
- **仓库（Registry）：** 存储和分发镜像的平台，如 Docker Hub（官方公共仓库）或私有仓库（如 Harbor）。

---

## 常用的 Docker 客户端命令

以下是常用的 Docker 客户端命令：

|**命令**|**功能**|**示例**|
|---|---|---|
|`docker run`|启动一个新的容器并运行命令|`docker run -d ubuntu`|
|`docker ps`|列出当前正在运行的容器|`docker ps`|
|`docker ps -a`|列出所有容器（包括已停止的容器）|`docker ps -a`|
|`docker build`|使用 Dockerfile 构建镜像|`docker build -t my-image .`|
|`docker images`|列出本地存储的所有镜像|`docker images`|
|`docker pull`|从 Docker 仓库拉取镜像|`docker pull ubuntu`|
|`docker push`|将镜像推送到 Docker 仓库|`docker push my-image`|
|`docker exec`|在运行的容器中执行命令|`docker exec -it container_name bash`|
|`docker stop`|停止一个或多个容器|`docker stop container_name`|
|`docker start`|启动已停止的容器|`docker start container_name`|
|`docker restart`|重启一个容器|`docker restart container_name`|
|`docker rm`|删除一个或多个容器|`docker rm container_name`|
|`docker rmi`|删除一个或多个镜像|`docker rmi my-image`|
|`docker logs`|查看容器的日志|`docker logs container_name`|
|`docker inspect`|获取容器或镜像的详细信息|`docker inspect container_name`|
|`docker exec -it`|进入容器的交互式终端|`docker exec -it container_name /bin/bash`|
|`docker network ls`|列出所有 Docker 网络|`docker network ls`|
|`docker volume ls`|列出所有 Docker 卷|`docker volume ls`|
|`docker-compose up`|启动多容器应用（从 `docker-compose.yml` 文件）|`docker-compose up`|
|`docker-compose down`|停止并删除由 `docker-compose` 启动的容器、网络等|`docker-compose down`|
|`docker info`|显示 Docker 系统的详细信息|`docker info`|
|`docker version`|显示 Docker 客户端和守护进程的版本信息|`docker version`|
|`docker stats`|显示容器的实时资源使用情况|`docker stats`|
|`docker login`|登录 Docker 仓库|`docker login`|
|`docker logout`|登出 Docker 仓库|`docker logout`|

**常用选项说明:**

- **`-d`**：后台运行容器，例如 `docker run -d ubuntu`。
- **`-it`**：以交互式终端运行容器，例如 `docker exec -it container_name bash`。
- **`-t`**：为镜像指定标签，例如 `docker build -t my-image .`。


# 尚硅谷Docker速通系列笔记

## 1. 安装  
  
国内常⻅云平台：●阿⾥云、腾讯云、华为云、⻘云......使⽤ CentOS 7.9WindTerm下载：https://github.com/kingToolbox/WindTerm/releases/download/2.6.0/WindTerm_2.6.1_Windows_Portable_x86_64.zip  
  
```shell
# 移除旧版本docker
sudo yum remove docker \
 docker-client \
 docker-client-latest \
 docker-common \
 docker-latest \
 docker-latest-logrotate \
 docker-logrotate \
 docker-engine
# 配置docker yum源。
sudo yum install -y yum-utils
sudo yum-config-manager \
--add-repo \
http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# 安装 最新 docker
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-pl
ugin docker-compose-plugin
# 启动& 开机启动docker； enable + start ⼆合⼀
systemctl enable docker --now
# 配置加速
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
 "registry-mirrors": ["https://mirror.ccs.tencentyun.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker

```
  
## 2. 命令  
  
```shell
#查看运⾏中的容器
docker ps
#查看所有容器
docker ps -a
#搜索镜像
docker search nginx
#下载镜像
docker pull nginx
#下载指定版本镜像
docker pull nginx:1.26.0
#查看所有镜像
docker images
#删除指定id的镜像
docker rmi e784f4560448
#运⾏⼀个新容器
docker run nginx
#停⽌容器
docker stop keen_blackwell
#启动容器
docker start 592
#重启容器
docker restart 592
#查看容器资源占⽤情况
docker stats 592
#查看容器⽇志
docker logs 592
#删除指定容器
docker rm 592
#强制删除指定容器
docker rm -f 592
# 后台启动容器
docker run -d --name mynginx nginx
# 后台启动并暴露端⼝
docker run -d --name mynginx -p 80:80 nginx
# 进⼊容器内部
docker exec -it mynginx /bin/bash
# 提交容器变化打成⼀个新的镜像
docker commit -m "update index.html" mynginx mynginx:v1.0
# 保存镜像为指定⽂件
docker save -o mynginx.tar mynginx:v1.0
# 删除多个镜像
docker rmi bde7d154a67f 94543a6c1aef e784f4560448

# 加载镜像
docker load -i mynginx.tar
# 登录 docker hub
docker login
# 重新给镜像打标签
docker tag mynginx:v1.0 leifengyang/mynginx:v1.0
# 推送镜像
docker push leifengyang/mynginx:v1.0
```
  
## 3. 存储  
  
两种⽅式，注意区分：  
  
⽬录挂载：   -v /app/nghtml:/usr/share/nginx/html  
  
卷映射： -v ngconf:/etc/nginx  
  
```
docker run -d -p 99:80 \  
-v /app/nghtml:/usr/share/nginx/html \  
-v ngconf:/etc/nginx \  
--name app03 \  
nginx  
```
  
## 4. ⽹络  
  
创建⾃定义⽹络，实现主机名作为稳定域名访问。  
  
### 4.1. Redis主从同步集群  

![](https://setsailtowardstianhan.ip-ddns.com/blog/677d0e6caed958fca2c7655608812b30.png)


```shell
#⾃定义⽹络
docker network create mynet
#主节点
docker run -d -p 6379:6379 \
-v /app/rd1:/bitnami/redis/data \
-e REDIS_REPLICATION_MODE=master \
-e REDIS_PASSWORD=123456 \
--network mynet --name redis01 \
bitnami/redis
#从节点
docker run -d -p 6380:6379 \
-v /app/rd2:/bitnami/redis/data \
-e REDIS_REPLICATION_MODE=slave \
-e REDIS_MASTER_HOST=redis01 \
-e REDIS_MASTER_PORT_NUMBER=6379 \
-e REDIS_MASTER_PASSWORD=123456 \
-e REDIS_PASSWORD=123456 \
--network mynet --name redis02 \
bitnami/redis

```

4.2 MySQL

```shell
docker run -d -p 3306:3306 \
-v /app/myconf:/etc/mysql/conf.d \
-v /app/mydata:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=123456 \
mysql:8.0.37-debian
```

## 5. Docker Compose  


![](https://setsailtowardstianhan.ip-ddns.com/blog/627c8764b5e3964dd02dc1917d691924.png)


![](https://setsailtowardstianhan.ip-ddns.com/blog/2df4113d0dea9d0f7fe3f79cb76be092.png)


![](https://setsailtowardstianhan.ip-ddns.com/blog/103be6957ba1ed87dd04190e665f8e4e.png)

5.1. 命令式安装  
  
```shell
#创建⽹络
docker network create blog
#启动mysql
docker run -d -p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=123456 \
-e MYSQL_DATABASE=wordpress \
-v mysql-data:/var/lib/mysql \
-v /app/myconf:/etc/mysql/conf.d \
--restart always --name mysql \
--network blog \
mysql:8.0
#启动wordpress
docker run -d -p 8080:80 \
-e WORDPRESS_DB_HOST=mysql \
-e WORDPRESS_DB_USER=root \
-e WORDPRESS_DB_PASSWORD=123456 \
-e WORDPRESS_DB_NAME=wordpress \
-v wordpress:/var/www/html \
--restart always --name wordpress-app \
--network blog \
wordpress:latest

```
  
5.2. compose.yaml  
  
```yaml
name: myblog
services:
 mysql:
 container_name: mysql
 image: mysql:8.0
 ports:
 - "3306:3306"
 environment:
 - MYSQL_ROOT_PASSWORD=123456
 - MYSQL_DATABASE=wordpress
 volumes:
 - mysql-data:/var/lib/mysql
 - /app/myconf:/etc/mysql/conf.d
 restart: always
 networks:
 - blog
 wordpress:
 image: wordpress
 ports:
 - "8080:80"
 environment:
 WORDPRESS_DB_HOST: mysql
 WORDPRESS_DB_USER: root
 WORDPRESS_DB_PASSWORD: 123456
 WORDPRESS_DB_NAME: wordpress
 volumes:
 - wordpress:/var/www/html
 restart: always
 networks:
 - blog
 depends_on:
 - mysql
volumes:
 mysql-data:
 wordpress:
networks:
 blog:

```
  
5.3. 特性  
  
●  增量更新：修改 Docker Compose ⽂件。重新启动应⽤。只会触发修改项的重新启动。  
●  数据不删：默认就算down了容器，所有挂载的卷不会被移除。⽐较安全  

## 6. Dockerfile  
  
```
FROM openjdk:17
LABEL author=leifengyang
COPY app.jar /app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app.jar"]

```
  

![](https://setsailtowardstianhan.ip-ddns.com/blog/ab8595bd7f4b13313f8c43c2f6819838.png)


![](https://setsailtowardstianhan.ip-ddns.com/blog/3a7eaf3483843729ed4c9c79d031e7ae.png)

容器层存储用户数据
## 附录——⼀键安装超多中间件  

![](https://setsailtowardstianhan.ip-ddns.com/blog/6bbb11798766aaffbcecf178c2a8471e.png)

OpenSearch是ElasticSearch的开源版本

![](https://setsailtowardstianhan.ip-ddns.com/blog/44dd85d103992db45725a0a9b026fe41.png)


```shell
#Disable memory paging and swapping performance  
sudo swapoff -a  
  
# Edit the sysctl config file  
sudo vi /etc/sysctl.conf  
  
# Add a line to define the desired value  
# or change the value if the key exists,  
# and then save your changes.  
vm.max_map_count=262144  
  
# Reload the kernel parameters using sysctl  
sudo sysctl -p  
  
# Verify that the change was applied by checking the value  
cat /proc/sys/vm/max_map_count  
```

7.1. yaml 

注意：将下⾯⽂件中 kafka 的 119.45.147.122 改为你⾃⼰的服务器IP。 准备⼀个 compose.yaml ⽂件，内容如下：

```
name: devsoft
services:
 redis:
 image: bitnami/redis:latest
 restart: always
 container_name: redis
 environment:
 - REDIS_PASSWORD=123456
 ports:
 - '6379:6379'
 volumes:
 - redis-data:/bitnami/redis/data
 - redis-conf:/opt/bitnami/redis/mounted-etc
 mysql:
 image: mysql:8.0.31
 restart: always
 container_name: mysql
 environment:
 - MYSQL_ROOT_PASSWORD=123456
 ports:
 - '3306:3306'
 - '33060:33060'
 volumes:
 - mysql-conf:/etc/mysql/conf.d
 - mysql-data:/var/lib/mysql
 rabbit:
 image: rabbitmq:3-management
 restart: always
 container_name: rabbitmq
 ports:
 - "5672:5672"
 - "15672:15672"
 environment:
 - RABBITMQ_DEFAULT_USER=rabbit
 - RABBITMQ_DEFAULT_PASS=rabbit
 - RABBITMQ_DEFAULT_VHOST=dev
 volumes:
 - rabbit-data:/var/lib/rabbitmq
 - rabbit-app:/etc/rabbitmq
 opensearch-node1:
 image: opensearchproject/opensearch:2.13.0
 container_name: opensearch-node1
 environment:
- cluster.name=opensearch-cluster # Name the cluster
 - node.name=opensearch-node1 # Name the node that will run in this
container
 - discovery.seed_hosts=opensearch-node1,opensearch-node2 # Nodes t
o look for when discovering the cluster
 - cluster.initial_cluster_manager_nodes=opensearch-node1,opensearch
-node2 # Nodes eligibile to serve as cluster manager
 - bootstrap.memory_lock=true # Disable JVM heap memory swapping
 - "OPENSEARCH_JAVA_OPTS=-Xms512m -Xmx512m" # Set min and max JVM he
ap sizes to at least 50% of system RAM
 - "DISABLE_INSTALL_DEMO_CONFIG=true" # Prevents execution of bundle
d demo script which installs demo certificates and security configuration
s to OpenSearch
 - "DISABLE_SECURITY_PLUGIN=true" # Disables Security plugin
 ulimits:
 memlock:
 soft: -1 # Set memlock to unlimited (no soft or hard limit)
 hard: -1
 nofile:
 soft: 65536 # Maximum number of open files for the opensearch use
r - set to at least 65536
 hard: 65536
 volumes:
 - opensearch-data1:/usr/share/opensearch/data # Creates volume call
ed opensearch-data1 and mounts it to the container
 ports:
 - 9200:9200 # REST API
 - 9600:9600 # Performance Analyzer
 opensearch-node2:
 image: opensearchproject/opensearch:2.13.0
 container_name: opensearch-node2
 environment:
 - cluster.name=opensearch-cluster # Name the cluster
 - node.name=opensearch-node2 # Name the node that will run in this
container
 - discovery.seed_hosts=opensearch-node1,opensearch-node2 # Nodes t
o look for when discovering the cluster
 - cluster.initial_cluster_manager_nodes=opensearch-node1,opensearch
-node2 # Nodes eligibile to serve as cluster manager
 - bootstrap.memory_lock=true # Disable JVM heap memory swapping
 - "OPENSEARCH_JAVA_OPTS=-Xms512m -Xmx512m" # Set min and max JVM he
ap sizes to at least 50% of system RAM
 - "DISABLE_INSTALL_DEMO_CONFIG=true" # Prevents execution of bundle
d demo script which installs demo certificates and security configuration
s to OpenSearch
 - "DISABLE_SECURITY_PLUGIN=true" # Disables Security plugin
 ulimits:

ock:
 soft: -1 # Set memlock to unlimited (no soft or hard limit)
 hard: -1
 nofile:
 soft: 65536 # Maximum number of open files for the opensearch use
r - set to at least 65536
 hard: 65536
 volumes:
 - opensearch-data2:/usr/share/opensearch/data # Creates volume call
ed opensearch-data2 and mounts it to the container
 opensearch-dashboards:
 image: opensearchproject/opensearch-dashboards:2.13.0
 container_name: opensearch-dashboards
 ports:
 - 5601:5601 # Map host port 5601 to container port 5601
 expose:
 - "5601" # Expose port 5601 for web access to OpenSearch Dashboards
 environment:
 - 'OPENSEARCH_HOSTS=["http://opensearch-node1:9200","http://opensea
rch-node2:9200"]'
 - "DISABLE_SECURITY_DASHBOARDS_PLUGIN=true" # disables security das
hboards plugin in OpenSearch Dashboards
 zookeeper:
 image: bitnami/zookeeper:3.9
 container_name: zookeeper
 restart: always
 ports:
 - "2181:2181"
 volumes:
 - "zookeeper_data:/bitnami"
 environment:
 - ALLOW_ANONYMOUS_LOGIN=yes
 kafka:
 image: 'bitnami/kafka:3.4'
 container_name: kafka
 restart: always
 hostname: kafka
 ports:
 - '9092:9092'
 - '9094:9094'
 environment:
 - KAFKA_CFG_NODE_ID=0
 - KAFKA_CFG_PROCESS_ROLES=controller,broker
 - KAFKA_CFG_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:9093,EXTERNA
L://0.0.0.0:9094

- KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://kafka:9092,EXTERNAL://
119.45.147.122:9094
 - KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP=CONTROLLER:PLAINTEXT,EXT
ERNAL:PLAINTEXT,PLAINTEXT:PLAINTEXT
 - KAFKA_CFG_CONTROLLER_QUORUM_VOTERS=0@kafka:9093
 - KAFKA_CFG_CONTROLLER_LISTENER_NAMES=CONTROLLER
 - ALLOW_PLAINTEXT_LISTENER=yes
 - "KAFKA_HEAP_OPTS=-Xmx512m -Xms512m"
 volumes:
 - kafka-conf:/bitnami/kafka/config
 - kafka-data:/bitnami/kafka/data
 kafka-ui:
 container_name: kafka-ui
 image: provectuslabs/kafka-ui:latest
 restart: always
 ports:
 - 8080:8080
 environment:
 DYNAMIC_CONFIG_ENABLED: true
 KAFKA_CLUSTERS_0_NAME: kafka-dev
 KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: kafka:9092
 volumes:
 - kafkaui-app:/etc/kafkaui
 nacos:
 image: nacos/nacos-server:v2.3.1
 container_name: nacos
 ports:
 - 8848:8848
 - 9848:9848
 environment:
 - PREFER_HOST_MODE=hostname
 - MODE=standalone
 - JVM_XMX=512m
 - JVM_XMS=512m
 - SPRING_DATASOURCE_PLATFORM=mysql
 - MYSQL_SERVICE_HOST=nacos-mysql
 - MYSQL_SERVICE_DB_NAME=nacos_devtest
 - MYSQL_SERVICE_PORT=3306
 - MYSQL_SERVICE_USER=nacos
 - MYSQL_SERVICE_PASSWORD=nacos
 - MYSQL_SERVICE_DB_PARAM=characterEncoding=utf8&connectTimeout=1000
&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serve
rTimezone=Asia/Shanghai&allowPublicKeyRetrieval=true
 - NACOS_AUTH_IDENTITY_KEY=2222
 - NACOS_AUTH_IDENTITY_VALUE=2xxx
 - NACOS_AUTH_TOKEN=SecretKey012345678901234567890123456789012345678
901234567890123456789

 - NACOS_AUTH_ENABLE=true
 volumes:
 - /app/nacos/standalone-logs/:/home/nacos/logs
 depends_on:
 nacos-mysql:
 condition: service_healthy
 nacos-mysql:
 container_name: nacos-mysql
 build:
 context: .
 dockerfile_inline: |
 FROM mysql:8.0.31
 ADD https://raw.githubusercontent.com/alibaba/nacos/2.3.2/distrib
ution/conf/mysql-schema.sql /docker-entrypoint-initdb.d/nacos-mysql.sql
 RUN chown -R mysql:mysql /docker-entrypoint-initdb.d/nacos-mysql.
sql
 EXPOSE 3306
 CMD ["mysqld", "--character-set-server=utf8mb4", "--collation-ser
ver=utf8mb4_unicode_ci"]
 image: nacos/mysql:8.0.30
 environment:
 - MYSQL_ROOT_PASSWORD=root
 - MYSQL_DATABASE=nacos_devtest
 - MYSQL_USER=nacos
 - MYSQL_PASSWORD=nacos
 - LANG=C.UTF-8
 volumes:
 - nacos-mysqldata:/var/lib/mysql
 ports:
 - "13306:3306"
 healthcheck:
 test: [ "CMD", "mysqladmin" ,"ping", "-h", "localhost" ]
 interval: 5s
 timeout: 10s
 retries: 10
 prometheus:
 image: prom/prometheus:v2.52.0
 container_name: prometheus
 restart: always
 ports:
 - 9090:9090
 volumes:
 - prometheus-data:/prometheus
 - prometheus-conf:/etc/prometheus
 grafana:
 image: grafana/grafana:10.4.2
 container_name: grafana

start: always
 ports:
 - 3000:3000
 volumes:
 - grafana-data:/var/lib/grafana
volumes:
 redis-data:
 redis-conf:
 mysql-conf:
 mysql-data:
 rabbit-data:
 rabbit-app:
 opensearch-data1:
 opensearch-data2:
 nacos-mysqldata:
 zookeeper_data:
 kafka-conf:
 kafka-data:
 kafkaui-app:
 prometheus-data:
 prometheus-conf:
 grafana-data:

```


7.2. 启动  

```shell
# 在 compose.yaml ⽂件所在的⽬录下执⾏
docker compose up -d
# 等待启动所有容器
```

tip：如果重启了服务器，可能有些容器会启动失败。再执⾏⼀遍 docker compose up -d 即可。 所有程序都可运⾏成功，并且不会丢失数据。请放⼼使⽤。

7.3. 访问 

zookeeper可视化⼯具下载： https://github.com/vran-dev/PrettyZoo/releases/download/v2.1.1/prettyZoo-win.zip

redis可视化⼯具下载： https://github.com/qishibo/AnotherRedisDesktopManager/releases/download/v1.6.4/An other-Redis-Desktop-Manager.1.6.4.exe

![](https://setsailtowardstianhan.ip-ddns.com/blog/70326cc8c08484f81d0cc70ae40fe008.png)









