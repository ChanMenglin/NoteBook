# Docker

> 使用的是版本 1.13 或更高版本。  
> **Docker** - [Docker](https://www.docker.com/) | 
[Github](https://github.com/docker) | 
[Open Source](https://www.docker.com/community/open-source) | 
[中文网](https://www.docker-cn.com/) | 
[Doc](https://docs.docker.com/) | 
[中文文档](https://docs.docker-cn.com/) | 
[Hub](https://hub.docker.com/) | 
[Store](https://store.docker.com/) | 
[中文社区](http://www.docker.org.cn/index.html)  
> 
> **Open Source**  
> 
> **Play with Docker** - [Page](https://labs.play-with-docker.com/) | 
[Github](https://github.com/play-with-docker/play-with-docker) 体验到在云中拥有免费的Alpine Linux虚拟机，您可以在其中构建和运行Docker容器，甚至可以使用Swarm模式等Docker功能创建集群。  
> **Moby** - [Page](https://mobyproject.org/) | 
[Github](https://github.com/moby/moby) Docker创建的一个开源项目，用于启用和加速软件容器化。
它提供了工具包组件的“乐高集”，用于将它们组装到基于容器的自定义系统中的框架，以及所有容器爱好者和专业人员实验和交换想法的地方。组件包括容器构建工具，容器注册表，编排工具，运行时等，这些可以与其他工具和项目一起用作构建块。  
> 
> **Docker image**  
> 
> [Nextcloud](https://github.com/nextcloud/docker) 所有数据的安全之家。 根据您的条款，从任何设备访问和共享您的文件，日历，联系人，邮件等。  

## Docker 常用命令

* `docker -v`/`docker --version` 查看当前安装的 Docker 版本
* `docker container ls`/`docker ps` 查看所有正在运行的容器的列表
* `docker ps -a` 查看所有容器的列表，甚至包含未运行的容器
* `docker run hello-world` 对环境进行快速的测试运行
* `docker images`/`docker image ls` 查看已构建的镜像
* `docker build -t <name>` 使用此目录的 Dockerfile 创建镜像
* `docker run -p 4000:80 <name>` 运行端口 4000 到 90 的“友好名称”映射
* `docker run -d -p 4000:80 <name>` 分离模式下
* `docker stop <hash>` 平稳地停止指定的容器
* `docker kill <hash>` 强制关闭指定的容器
* `docker rm <hash>` 从此机器中删除指定的容器
* `docker rm $(docker ps -a -q)` 从此机器中删除所有容器
* `docker images -a` 显示此机器上的所有镜像
* `docker rmi <imagename>` 从此机器中删除指定的镜像
* `docker rmi $(docker images -q)` 从此机器中删除所有镜像
* `docker login` 使用您的 Docker 凭证登录此 CLI 会话
* `docker tag <image> username/repository:tag` 标记 `<image>` 以上传到镜像库
* `docker push username/repository:tag` 将已标记的镜像上传到镜像库
* `docker run username/repository:tag` 运行镜像库中的镜像