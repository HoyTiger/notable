---
title: docker 笔记
created: '2022-06-17T06:56:42.587Z'
modified: '2022-06-17T07:22:55.051Z'
---

# docker 笔记
## 参数说明

## 常用命令
### 获取容器
```docker
docker pull ubuntu #
docker run ubuntu # 如果不存在Ubuntu本地镜像，会首先获取容器
```

### 启动容器
```
docker run -it ubuntu /bin/bash
```
参数说明：

- -i: 交互式操作。
- -t: 终端。
- ubuntu: ubuntu 镜像。
- /bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。
- 要退出终端，直接输入 exit:

### 后台运行
在大部分的场景下，我们希望 docker 的服务是在后台运行的，我们可以过 -d 指定容器的运行模式。

### Dockerfile
Dockerfile 中的 FROM 指令用于指定要构建的镜像的基础镜像。它通常是 Dockerfile 中的第一条指令。

Dockerfile 中的 RUN 指令用于在镜像中执行命令，这会创建新的镜像层。每个 RUN 指令创建一个新的镜像层。

Dockerfile 中的 COPY 指令用于将文件作为一个新的层添加到镜像中。通常使用 COPY 指令将应用代码赋值到镜像中。

Dockerfile 中的 EXPOSE 指令用于记录应用所使用的网络端口。

Dockerfile 中的 ENTRYPOINT 指令用于指定镜像以容器方式启动后默认运行的程序。
