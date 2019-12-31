# Docker 练习

## Docker是什么

### Docker概念



Docker 是世界领先的软件容器平台。

Docker 使用 Google 公司推出的 Go 语言  进行开发实现，基于 Linux 内核 的cgroup，namespace，以及 AUFS 类的 UnionFS 等技术，对进程进行封装隔离，属于操作系统层面的虚拟化技术。 由于隔离的进程独立于宿主和其它的隔离的进 程，因此也称其为容器。Docker 最初实现是基于 LXC.

Docker 能够自动执行重复性任务，例如搭建和配置开发环境，从而解放了开发人员以便他们专注在真正重要的事情上，构建杰出的软件。

用户可以方便地创建和使用容器，把自己的应用放入容器。容器还可以进行版本管理、复制、分享、修改，就像管理普通的代码一样。



## Docker 应用

#### 1. 使用 [express -e ]命令初始化一个Node项目

express -e  <项目名称> 



#### 2. 在根目录创建 Dockerfile 文件 并 添加以下内容



`# Dockerfile `
`FROM node:10.0` 

` # 在容器中创建一个目录 `
`RUN mkdir -p /app`

`# 定位到容器的工作目录 `
`WORKDIR /app `

`# RUN/COPY 是分层的，package.json 提前，只要没修改，就不会重新安装包`
`COPY package.json /app/package.json`
`RUN cd /app`
`RUN npm i `

`# 把当前目录下的所有文件拷贝到 Image 的 /app 目录下 `
`COPY . /app  `

`EXPOSE 3000`

`CMD npm start ` 



#### 3.构建项目

docker build -t  <镜像名称> . 

#### 4. 创建容器并运行

docker  run  --name dockerTest -d -p 3000:3000 dockerTest



#### 5. 查看运行结果

curl   localhost:3000   或者   浏览器查看 



出现 Express  字样成功运行



#### 6.进入容器

docker ls -a   查看所有容器，包括当前容器的id 

docker exec -it <id> bash



#### 7. 查看运行日志

docker logs -f  <id>