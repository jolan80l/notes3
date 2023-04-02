# 学习目的

就个人的目前情况来说，Docker学习并不是一个迫在眉睫的事情，公司有自己的容器化工具，不需要过多的关注这块的内容。但是为什么要学它呢？主要目的是为了学习Elasticsearch这个工具，要使用它不可避免的需要在电脑上安装它的运行环境。今天学这个明天学那个，电脑上安装了很多软件，基本很少使用，又不想卸载。在这种情况下，想到了使用Docker来管理这些软件，所以这个笔记命名为Docker_Get_started——Docker的快速入门。如果以后有必要的话，再做更深入的学习。Docker是什么，参考文章：https://zhuanlan.zhihu.com/p/187505981

# docker安装

docker本身需要依赖操作系统的环境，所以docker的安装也要看具体安装到什么操作系统下，比如Linux、windows、mac等。我的电脑是mac操作系统，所以选择mac桌面版的docker进行安装。在这里可以找到桌面版docker的安装包：https://www.docker.com/products/docker-desktop/。mac版本的安装只要双击下载好的Docker.dmg文件，将Docker拖拽到应用程序即可。安装完成后，在Finder的应用程序中就可以找到Docker。

如果使用的是windows操作系统，可以参考这个文章的简介和安装部分：https://docker.easydoc.net/doc/81170005/cCewZWoN/lTKfePfP

# 镜像加速

需要翻山越岭，给拉取镜像提个速。

Docker 中国官方镜像	https://registry.docker-cn.com

DaoCloud 镜像站	http://f1361db2.m.daocloud.io


Azure 中国镜像	https://dockerhub.azk8s.cn

科大镜像站	https://docker.mirrors.ustc.edu.cn

阿里云	https://ud6340vz.mirror.aliyuncs.com

七牛云	https://reg-mirror.qiniu.com

网易云	https://hub-mirror.c.163.com

腾讯云	https://mirror.ccs.tencentyun.com

![avatar](img/1.png)

# 使用docker安装redis

为什么是安装redis？前面不是说学习Elasticsearch？没办法，视频教程里面就是这样教的，而且本文的目的是为了学习Docker，redis还是Elasticsearch并不重要。

安装完docker后，再安装redis镜像只需要一个命令即可；

```shell
docker run -d -p 6379:6379 --name redis6.2.6 redis:6.2.6
```

![avatar](img/3.jpg)

- -d：这个命令表示后台运行

- -p：这个命令表示将docker中的6379端口映射到宿主机的6379端口

- --name：这个命令表示给镜像明明

- redis:6.2.6：这个表示拉取redis的镜像，版本号是6.2.6

想要了解docker的其他命令，可以在docker的官网文档中查找，文档地址：https://docs.docker.com/。比如要搜索run命令，如下图所示。

![avatar](img/2.jpg)

当命令执行成功，返回docker的控制台，查看容器和镜像情况。

![avatar](img/4.jpg)

redis已经通过docker容器运行起来了，如果本地安装了redis客户端，可以直接在本地访问，也可以在docker终端中访问redis。

- 本地方式

```shell
redis-cli  
127.0.0.1:6379> set docker_test '20230402'
OK
127.0.0.1:6379>
```

- 终端方式

![avatar](img/5.jpg)

![avatar](img/6.jpg)

# 安装Elasticsearch

```shell
docker pull docker.io/elasticsearch:版本号

```








