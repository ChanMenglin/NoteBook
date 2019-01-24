# Docker

> 使用的是版本 1.13 或更高版本。

## Docker 常用命令

* `docker -v`/`docker --version` 查看当前安装的 Docker 版本
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