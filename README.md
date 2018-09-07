# DevDependent
开发依赖的docker服务

- Mac环境下docker启用API

```bash
docker run -d -v /var/run/docker.sock:/var/run/docker.sock -p 2376:2375 bobrik/socat TCP4-LISTEN:2375,fork,reuseaddr UNIX-CONNECT:/var/run/docker.sock
```

- mysql启动命令：

```bash
docker run -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 --name mysql -d mysql:5.7.20
```

```bash
docker run --name postgres -e POSTGRES_PASSWORD=123456 -p 5432:5432 -d postgres:10.5
```

- redis启动命令：

```bash
docker run -p 6379:6379 --name redis -d redis

docker run -p 6379:6379 --name redis -d redis --requirepass "123456"
```

- zookeeper启动命令

```bash
docker run -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zookeeper -d zookeeper
```

- consul

```
docker run -d -p 8500:8500 --name consul  consul agent -server -bootstrap -client=0.0.0.0 -ui
```

- influxdb

```
docker pull influxdb:1.6

docker run -p 8086:8086 --name influxdb -d influxdb:1.6

docker run -p 8086:8086 -p 8083:8083 -e ADMIN_USER="root" -e INFLUXDB_INIT_PWD="123456" -e PRE_CREATE_DB="metrics" --name influxdb -d influxdb:1.6

// 创建数据库 metrics为数据库名字
curl -G -XPOST http://localhost:8086/query --data-urlencode "q=CREATE DATABASE metrics"

```

- grafana

```
// 默认账号 admin 密码 admin
docker run -d --name=grafana -p 3000:3000 grafana/grafana

```

- prometheus

```
docker pull prom/prometheus

docker run --name prometheus -p 9090:9090 -d prom/prometheus

docker run -p 9090:9090 -v /tmp/prometheus-data:/prometheus-data prom/prometheus

```
