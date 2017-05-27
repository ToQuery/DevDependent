# DevDependent
开发依赖的docker服务

- Mac环境下docker启用API

```bash
docker run -d -v /var/run/docker.sock:/var/run/docker.sock -p 2376:2375 bobrik/socat TCP4-LISTEN:2375,fork,reuseaddr UNIX-CONNECT:/var/run/docker.sock
```

- mysql启动命令：

```bash
docker run -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 --name mysql -d mysql
```

- redis启动命令：

```bash
docker run -p 6379:6379 --name redis -d redis
```

- zookeeper启动命令

```bash
docker run -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zookeeper -d zookeeper
```
