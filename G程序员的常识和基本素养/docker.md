# Docker
- Docker 能做什么?  
  方便的解决环境变量的配置问题.  
  语言编译器, 解释器, 依赖.  
  它可以复制原始环境.  

- Docker 和虚拟机相比, 有什么差异?  
  虚拟机占用资源大, 启动速度慢, 安装麻烦  

- Linux 容器是什么?  
  一种虚拟化机技术, 对进程进行隔离, 对正常的进程套一层壳.  
  有着启动快, 占用资源小而且可以共享, 体积小的优点.  

- Docker 有什么优势?  
  Docker是 Linux 容器的一种封装, 提供简单好用的容器接口. 白话: 非专业人士用Linux容器更方便了, 难度降低了.  

- Docker 的使用场景是什么?  

  TODO

- Docker 如何安装和启动?  
  STFW  

- docker的理念

  一个容器运行一个进程，而且这个容器应该是一次性的，有单独的卷来保证数据持久性！



# 在Linux下安装

wget -qO- https:*//get.docker.com/ | sh*

docker --version # 检验一下



# 修改为国内仓库

解决方案：
在MacOS 下，修改`~/.docker/daemon.json`文件，在后面加入：

```
{
    "registry-mirrors":["https://3laho3y3.mirror.aliyuncs.com"]
}
```

https://3laho3y3.mirror.aliyuncs.com 测试可用，2020-03-30 10:54:01

有的时候国内仓库不可用，**使用以下命令先测试一下**：

docker pull  [test-registry-mirrors]/library/hello-world



备用：

https://yqo68yqi.mirror.aliyuncs.com   可用
https://blog.csdn.net/u012055638/article/details/79803959

说明：这种加速仓库其实是每个用户自己申请可以建立私人仓库的，如果你不用上传自己的镜像，可以使用别人的加速仓库地址。



# image命令

```bash
docker image ls
```

- Image 文件是什么?  
  应用程序和依赖的打包.  
  通过一个 Image 可以生成 Docker 容器, 而且可以有多个实例同时运行.  
  还可以继承.  
  还是跨平台的, 太厉害了吧, 和 Java 一样!  
  在继承的基础上, 可以自我定制, 牛逼!  
  网上有 Image 仓库, Dockerhub, 还可以进行 Image 交易.  
- 如何下载Image 文件?  
  docker image pull library/hello-world  
  docker container run hello-world  
  docker container ls  [--all 表示所有] # 正在运行的container
  docker container kill 
- 如何制作 Image?  
  进入项目根目录  
  编写.dockerignore 文件,省略一些不想一起打包的文件  
  新建一个文本文件 Dockerfile,(PS:后缀还是文件名?)  
  写入一些 docker 脚本命令  
  使用docker image build -t IMAGENAME:VERSION  
  使用 docker image ls 查看文件  
- 运行 Image 和停止 Image ?  
  使用 docker container run -p OUTER_PORT:DOCKER_PORT -it[shell 互连]  [--rm:运行后自动删除] IMAGENAME:VERSION /bin/bash[启动 内部shell的命令 ]  
  docker container kill  CONTAINER_ID    
  还有docker contan
- CMD 命令是什么?  
  Docker 脚本最后一句话, 但是不能再run 命令后面加 shell 启动命令, 否则会覆盖



# container命令

docker container start [containerID]
docker container stop [containerID]  # 温柔中断
docker container kill [containerID]  # 暴力中断
docker container logs [containerID] # 查看日志
**docker container exec -it [containerID] /bin/bash** 连接到一个正在运行的程序




# 端口映射

因为我用的是MacOS, 而MacOS的 docker 其实是和 Linux系统下面的不一样的。



```bash
$ docker container run --rm -p 8000:3000 -it koa-demo /bin/bash
```

mac上因为系统限制ping不了docker的容器

所以可以设置-p 8080:80 把端口映射出来



`expose` 和 `ports` 都可以暴露容器的端口，区别是 expose 仅暴露给其他容器，而 ports 会暴露给其他容器和宿主机。

例如：

```
  app:
    restart: always
    build: .
    command: bash -c "python3 manage.py collectstatic --no-input && python3 manage.py migrate && gunicorn --timeout=30 --workers=4 --bind :8000 django_app.wsgi:application"
    volumes:
      - .:/code
      - static-volume:/code/collected_static
    expose:
      - "8000"
```

```
  db:
    image: mysql:5.7
    volumes:
      - "./mysql:/var/lib/mysql"
    ports:
      - "3306:3306"
```



# 参数解释

- `-d`：容器启动后，在后台运行。
- `--rm`：容器终止运行后，自动删除容器文件。
- `--name wordpressdb`：容器的名字叫做`wordpressdb`
- `--env MYSQL_ROOT_PASSWORD=123456`：向容器进程传入一个环境变量`MYSQL_ROOT_PASSWORD`，该变量会被用作 MySQL 的根密码。



# 示例命令讲解

docker run -d \
 -h mysql \
-v /data/mysql:/var/lib/mysql \
-p 3306:3306 \
--name mysql \
-e MYSQL_ROOT_PASSWORD=root \
mysql 

> -h 设定主机名

> -d,  --detach   Run container in background and print container ID

$sudo docker run 
--name phpadmin 
--link mysql:db  # db是别名
-p 9998:80 
-d 
phpmyadmin/phpmyadmin 



# Dockefile

下载加速

```shell
FROM python:3.7
ENV PYTHONUNBUFFERED 1

# 添加 Debian 清华镜像源
RUN echo \
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free\
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free\
deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free\
deb https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free\
    > /etc/apt/sources.list

RUN mkdir /code
WORKDIR /code
# 添加 pip 清华镜像源
RUN pip install pip -U -i https://pypi.tuna.tsinghua.edu.cn/simple
ADD requirements.txt /code/
# 添加 pip 清华镜像源
RUN pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
ADD . /code/
```

这个是豆瓣的

https://pypi.doubanio.com/simple

# docker compose

以一个 django app为例，同时启动了两个 container

```yml
version: "3"
services:
  app:
    restart: always
    build: .  # '点'代表当前目录, 必须包含一个 Dockerfile 文件,否则会报错
    command: "python3 manage.py runserver 0.0.0.0:8000"
    volumes:
      - .:/code
    ports: # HOST_PORT:CONTAINER_PORT
      - "8080:8000"
    depends_on:
    - db # 一旦使用depends_on, 其中的连接就不再使用端口转发机制，而是直接使用内部连接

  db:
    image: mysql:5.7
    volumes:
      - "./mysql:/var/lib/mysql"
      - ./mysql_conf:/etc/mysql/conf.d # 为了修改mysql的端口号，同时为了持久化自己的配置
    ports:
      - "3306:3306" # 这个port 是映射到 宿主机的port,但是好像 app 连接的还是 3306, 并没有经过端口转发!! 经过测试,确实如此!，这个转发仅仅是为了方便宿主机访问而已！！
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=django_app
```

./mysql_conf的目录

```
mysql_conf
└── port.cnf
```

port.conf的内容

```
[mysqld]
port=3307
```



通过以上的配置成功的修改MySQL的端口号



# 待解决的问题

如果我修改了源代码，那么源代码对应的 APP 镜像就需要重新构建，因为其中涉及把代码拷贝到 APP镜像里面去，但是构建一个镜像非常浪费时间（涉及到下载很多依赖的问题），不知道如何解决。





# Reference  

- 阮一峰的docker入门教程

  http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html

- Docker 微服务教程

  http://www.ruanyifeng.com/blog/2018/02/docker-wordpress-tutorial.html

- Docker-Django本地部署

  https://github.com/stacklens/django-docker-tutorial

- MacOS 的 docker 网络配置

  https://docs.docker.com/docker-for-mac/networking/

- 一篇特别好的docker 教程

  https://www.cnblogs.com/neptunemoon/p/6512121.html

- 注册阿里云加速地址，使用自己的私人镜像库

  https://www.jb51.net/article/118703.htm

- Linux下更换国内hub

  https://www.cnblogs.com/winstom/p/9521029.html

- 