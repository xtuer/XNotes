```
# 启动 docker
service docker start
service docker stop

# 拉取 docker image
docker pull busybox

# Container 中运行 image
docker run -t --rm biao/busybox ls -l /root
docker run -i -t --rm biao/busybox /bin/ash
docker run -d biao/busybox /bin/sh -c "while true; do date; sleep 1; done"
# -t: 在新容器内指定一个伪终端或终端
# -i: 允许你对容器内的标准输入 (STDIN) 进行交互
# -d: 后台运行容器
# --rm: Automatically remove the container when it exits, 退出后用 docker ps -a 看不到
docker ps
docker stop containerId
docker logs containerId

# 基于 image 创建自己的 image
docker build -t biao/busybox .

# 查看 container 的状态
docker ps -a

# 查看有哪些 image
docker images
```

```
# Dockerfile
FROM busybox
MAINTAINER biao
RUN mkdir /root/biao
RUN mkdir /root/xtuer
```

```
# Dockerfile
FROM php:7.0-apache
COPY src/ /www/html
EXPOSE 80

# Run image
docker run -p 80:8080 -v /Users/Biao/Desktop/foo/src/:/www/html hello-world
# -v 指在 Container 运行时 src 下的文件变化时自动复制到 html 文件夹中
```

Docker 容器使用: [http://www.runoob.com/docker/docker-container-usage.html](http://www.runoob.com/docker/docker-container-usage.html)

> **image 和 container 的关系:**
>
> * image 相当于程序的安装包
>
> * container 相当于安装后的程序，同一个安装包每安装一次就会出现一个新的安装后的程序，不是覆盖\(相当于选择不同的安装路径\)
>
> * docker run image 运行一次就出现一个新的 container，停止的 container 可以使用 start 再次运行，start 不会创建新的 container



