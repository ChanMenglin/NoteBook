# Docker

> 使用的是版本 1.13 或更高版本。  

---
**Docker** - 
[Docker](https://www.docker.com/) | 
[中文网](https://www.docker-cn.com/) | 
[Doc](https://docs.docker.com/) | 
[中文文档](https://docs.docker-cn.com/) | 
[Github](https://github.com/docker) | 
[Docker Success Center](https://success.docker.com) | 
[Open Source](https://www.docker.com/community/open-source) | 
[Hub](https://hub.docker.com/) | 
[Store](https://store.docker.com/) | 
[中文社区](http://www.docker.org.cn/index.html) | 
[Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)  

---
**Open Source**  

**Play with Docker** - 
[Page](https://labs.play-with-docker.com/) | 
[Github](https://github.com/play-with-docker/play-with-docker) 
体验到在云中拥有免费的Alpine Linux虚拟机，您可以在其中构建和运行Docker容器，甚至可以使用Swarm模式等Docker功能创建集群。  
**awesome-docker** - 
[Page](https://awesome-docker.netlify.com) | 
[Github](https://github.com/veggiemonk/awesome-docker) 
Docker资源和项目的精选列表  
**Moby** - 
[Page](https://mobyproject.org/) | 
[Github](https://github.com/moby/moby) 
Docker创建的一个开源项目，用于启用和加速软件容器化。
它提供了工具包组件的“乐高集”，用于将它们组装到基于容器的自定义系统中的框架，以及所有容器爱好者和专业人员实验和交换想法的地方。组件包括容器构建工具，容器注册表，编排工具，运行时等，这些可以与其他工具和项目一起用作构建块。  
**Docker Official Images** - 
[Page](https://hub.docker.com/search/?q=&type=image) | 
[示例](https://docs.docker-cn.com/samples/) | 
[Github](https://github.com/docker-library/official-images) | 
[@Docker-Library](https://github.com/docker-library) 
Docker 官方 Images  
**oracle/docker-images** - 
[Page](https://developer.oracle.com/containers) | 
[Github](https://github.com/oracle/docker-images) 
Docker配置，图像以及Dockerfiles for Oracle产品和项目示例的官方来源  
**jupyter/docker-stacks** - 
[Page](https://jupyter-docker-stacks.readthedocs.io/en/latest/index.html) | 
[Github](https://github.com/jupyter/docker-stacks) 
包含Jupyter应用程序的可立即运行的Docker镜像  
**NVIDIA/nvidia-docker** - 
[Github](https://github.com/NVIDIA/nvidia-docker) 
利用NVIDIA GPU构建和运行Docker容器   

---
**Docker image**  

[Nextcloud](https://github.com/nextcloud/docker) 所有数据的安全之家。 根据您的条款，从任何设备访问和共享您的文件，日历，联系人，邮件等。  

## Docker 常用命令

**基础**  

* `docker info` Docker 信息
* `docker -v`/`docker --version` 查看当前安装的 Docker 版本
* `docker run hello-world` 对环境进行快速的测试运行

**容器**  

* `docker container ls`/`docker ps` 查看所有正在运行的容器的列表
* `docker ps -a` 查看所有容器的列表，甚至包含未运行的容器
* `docker inspect <hash>` 查看容器所有的相关信息
* `docker rm <hash>` 从此机器中删除指定的容器
* `docker rm $(docker ps -a -q)` 从此机器中删除所有容器

**镜像**  

* `docker images -a` 显示此机器上的所有镜像
* `docker images`/`docker image ls` 查看已构建的镜像
* `docker build -t <name>` 使用此目录的 Dockerfile 创建镜像
* `docker run -p 4000:80 <name>` 运行端口 4000 到 90 的“友好名称”映射
* `docker run -d -p 4000:80 <name>` 分离模式下运行
* `docker run <username>/<repository>:<tag>` 运行镜像库中的镜像
* `docker stop <hash>` 平稳地停止指定的容器
* `docker kill <hash>` 强制关闭指定的容器
* `docker rmi <imagename>` 从此机器中删除指定的镜像
* `docker rmi $(docker images -q)` 从此机器中删除所有镜像

**账户 Hub**  

* `docker login` 使用您的 Docker 凭证登录此 CLI 会话
* `docker tag <username>/<repository>:<tag>` 标记 `<image>` 以上传到镜像库
* `docker push <username>/<repository>:<tag>` 将已标记的镜像上传到镜像库

**服务**  

* `docker swarm init` 需要先运行以下命令，然后才能使用 `docker stack deploy` 命令
* 


docker stack ls              # 列出此 Docker 主机上所有正在运行的应用
docker stack deploy -c <composefile> <appname>  # 运行指定的 Compose 文件
docker stack services <appname>       # 列出与应用关联的服务
docker stack ps <appname>   # 列出与应用关联的正在运行的容器
docker stack rm <appname>                             # 清除应用

## Dockerfile 命令

**Dockerfiles** - 
[blog](https://blog.jessfraz.com/post/docker-containers-on-the-desktop/) | 
[Github](https://github.com/jessfraz/dockerfiles) 
各种 Dockerfiles 

| 命令  | 用途  |
| :--: | :--: |
| FROME | base image |
| RUN   | 执行命令    |
| ADD   | 添加文件    |
| COPY  | 拷贝文件    |
| CMD   | 执行命令    |
| EXPOSE| 暴露来端口  |
| WORKDIR | 指定路径  |
| MAINTAINER | 维护者 |
| ENV   | 设定环境变量 |
| ENTRYPOINT | 容器入口|
| USER  | 指定用户    |
| VOLUME| mount point|

Dockerfile 示例：

```Dockerfile
# 将官方 Python 运行时用作父镜像
FROM python:2.7-slim

# 将工作目录设置为 /app
WORKDIR /app

# 将当前目录内容复制到位于 /app 中的容器中
ADD . /app

# 安装 requirements.txt 中指定的任何所需软件包
RUN pip install -r requirements.txt

# 使端口 80 可供此容器外的环境使用
EXPOSE 80

# 定义环境变量
ENV NAME World

# 在容器启动时运行 app.py
CMD ["python", "app.py"]
```