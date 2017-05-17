# DevDependent
开发依赖的docker服务

- mysql启动命令：

```shell
docker run -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 --name mysql -d mysql
```

- redis启动命令：

```shell
docker run -p 6379:6379 --name redis -d redis
```

- zookeeper启动命令

```shell
docker run -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zookeeper -d zookeeper
```
