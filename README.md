# DevDependent

本文档主要介绍相关基于docker的开发依赖服务，包含容器管理、数据库、缓存、监控等。不断完善。。。

## 容器相关服务

- ~~Linux(Mac)下启用dockerAPI，基于docker.sock~~（推荐下面的方式）

> 基于Docker镜像的方式在2376端口开放docker-api接口

```bash
docker run -d -v /var/run/docker.sock:/var/run/docker.sock -p 2376:2375 bobrik/socat TCP4-LISTEN:2375,fork,reuseaddr UNIX-CONNECT:/var/run/docker.sock
```

- 修改docker的daemon.json开启docker-api如下，配置hosts节点

```json
{
//  可信任的镜像仓库
//  "insecure-registries" : ["xxx.abc.com"],
//  镜像加速仓库
//  "registry-mirrors": ["http://xxxx.m.daocloud.io"],
    "hosts":["tcp://0.0.0.0:2375","unix:///var/run/docker.sock"],
}
```

- portainer 容器管理

```
docker volume create portainer_data
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

## 数据库相关服务

- mysql启动命令：

```bash
docker run -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306  --restart=always --name mysql -d mysql:5.7.20
```

- postgresql

```bash
docker run --name postgres -e POSTGRES_PASSWORD=123456 -p 5432:5432 -d postgres:10.5

docker run --name postgres -e POSTGRES_PASSWORD=123456 -p 54321:5432 -d postgres:9.4.19
```


- influxdb

```bash
docker pull influxdb:1.6

docker run -p 8086:8086 --name influxdb -d influxdb:1.6

docker run -p 8086:8086 -p 8083:8083 -e ADMIN_USER="root" -e INFLUXDB_INIT_PWD="123456" -e PRE_CREATE_DB="metrics" --name influxdb -d influxdb:1.6

// 创建数据库 metrics为数据库名字
curl -G -XPOST http://localhost:8086/query --data-urlencode "q=CREATE DATABASE metrics"
```

## 缓存相关服务

- redis启动命令：

```bash
docker run -p 6379:6379 --name redis -d redis

docker run -p 6379:6379 --name redis -d redis --requirepass "123456"
```

## 其他相关服务

- zookeeper启动命令

```bash
docker run -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zookeeper -d zookeeper
```

- consul

```bash
docker run -d -p 8500:8500 --name consul  consul agent -server -bootstrap -client=0.0.0.0 -ui
```


## 监控相关服务

- grafana

```bash
// 默认账号 admin 密码 admin
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

- prometheus

```bash
docker pull prom/prometheus

docker run --name prometheus -p 9090:9090 -d prom/prometheus

docker run -p 9090:9090 -v /tmp/prometheus-data:/prometheus-data prom/prometheus
```
