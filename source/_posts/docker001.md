---
title: docker001
tags: [docker]
toc: true
mathjax: true
date: 2019-06-14 21:09:32
categories: docker
---
+ docker 定义
docker 用Go语言实现，基于Linux内核的cgroup，namespace等技术，对进程进行封装隔离，属于操作系统层面的虚拟化技术。

+ docker优势
更高效的利用系统资源
更快速的启动
一致的运行环境
持续交付和部署
更轻松的迁移
便于维护和扩展

+ docker的基本概念
镜像 Image
一个特殊的文件系统，提供容器运行时所需的程序、库、资源、配置等文件。镜像不包含任何动态数据，在构建后不会改变。
容器 Container
容器是镜像运行时的实体，类似程序设计中的类和实例。容器实际是一个进程，但是拥有自己的root文件系统、网络配置、进程空间、用户ID空间。容器应该无状态化，容器存储层的生存周期和容器一样。所有写入操作，都应该使用数据卷或者绑定宿主目录。
仓库 Repository
一个仓库包含同一个软件不同版本的镜像。
```
docker pull repo:tag
docker run -it --rm ubuntu:18.04 bash
docker image ls (-a)
docker image ls ubuntu
docker image ls -f since=mongo:3.2 (before)
docker image ls -f lable=com.example.version=0.1
docker image ls --format "table {{.ID}}: {{.Repository}}\t{{.Tag}}"
docker system df
docker image ls -f dangling=true 显示虚悬镜像
docker image prune 删除虚悬镜像
docker run --name webserver -d -p 80:80 nginx
docker run --name webserver2 -d -p 81:80 nginx:v2
docker exec -it webserver bash
docker ps -a
docker stop id
docker restart id

不要使用dock commit 黑箱操作
使用dockerfile
mkdir docker_nginx1
touch Dockerfile
FROM nginx
RUN echo '<h1>Hello, Docker!</h1>' > /usr/share/nginx/html/index.html
```
每次run 都是一层，所以要合理节省层数，现在最多支持127层。

在dockerfile 目录执行构建：
`docker build -t nginx:v2 .`
最后一个参数是上下文路径，COPY命令中也指的是上下文目录中的package.json
`COPY ./package.json /app/`

使用.dockerignore 排除不需要作为上下文传递给Docker引擎的内容。

常见的

构建方法：
```
docker build -t nginx:v2 .
docker build https://github.com/example.git
docker build http://server/context.tar.gz
docker build - < Dockerfile
docker build - < context.tar.gz
```
+ Dockerfile 指令详解
> COPY 文件复制
+ COPY [--chown=<user>:<group>] <源路径> <目标路径>

> ADD 更高级的文件复制
+ 仅在需要自动解压的场合使用ADD
+ ADD 支持 tar 压缩文件，压缩格式为gzip, bzip2, xz
+ ADD [--chown=<user>:<group>] ubuntu.tar.gz /

> CMD
+ CMD <命令>
+ CMD [ "可执行文件", "参数1", "参数2"]

> ENTRYPOINT
+ 镜像像命令一样带参数
+ ENTRYPOINT [ "curl", "-s", "https://ip.cn"]
+ 应用运行前的准备工作
+ 比如需要切换到 redis 用户来启动
+ ENTRYPOINT [ "docker-entrypoint.sh" ]

> ENV 设置环境变量
+ ENV <key> <value>
+ ENV <key1>=<value1> <key2>=<value2> ...

> ARG 构建参数
+ ARG <参数名>[=<默认值>]
+ ARG 设置的构建环境的变量不会保留在容器运行时。

> VOLUME 定义匿名卷
+ 数据库等需要保存动态数据的应用，应保存在卷中
+ 指定为匿名卷的内容都不会记录到容器存储层
+ VOLUME <路径>
+ VOLUME ["<路径1>", "<路径2>" ...]

> EXPOSE 声明端口
+ EXPOSE <端口1> [<端口2>...]

> WORKDIR 指定工作目录
+ WORKDIR <工作目录路径>
```
docker 每一个RUN都是启动一个容器
RUN cd /app
RUN echo "hello" > world.txt
此处应该用WORKDIR
```

> USER 指定当前用户
+ USER <用户名>[:<用户组>]
```
RUN groupadd -r redis && useradd -r -g redis redis
USER redis
RUN [ "redis-server" ]
推荐直接使用gosu
RUN wget -o /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64" && chmod +x /usr/local/bin/gosu && gosu nobody true
CMD [ "exec", "gosu", "redis", "redis-server"]
```

> HEALTHCHECK 健康检查
+ HEALTHCHECK [选项] CMD <命令>
```
HEALTHCHECK --interval=5s --timeout=3s CMD curl -fs http://localhost/ || exit 1
```

> ONBUILD 为他人做嫁衣
```
FROM node:slim
RUN mkdir /app
WORKDIR /app
ONBUILD COPY ./package.json /app
ONBUILD RUN [ "npm", "install"]
ONBUILD COPY . /app/
CMD [ "npm", "start"]
```