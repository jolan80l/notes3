# 学习目的

就个人的目前情况来说，Docker学习并不是一个迫在眉睫的事情，公司有自己的容器化工具，不需要过多的关注这块的内容。但是为什么要学它呢？主要目的是为了学习Elasticsearch这个工具，要使用它不可避免的需要在电脑上安装它的运行环境。今天学这个明天学那个，电脑上安装了很多软件，基本很少使用，又不想卸载。在这种情况下，想到了使用Docker来管理这些软件，所以这个笔记命名为Docker_Get_started——Docker的快速入门。如果以后有必要的话，再做更深入的学习。Docker是什么，参考文章：https://zhuanlan.zhihu.com/p/187505981

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

```json
"registry-mirrors":[
        "https://registry.docker-cn.com",
        "https://docker.mirrors.ustc.edu.cn",
        "https://hub-mirror.c.163.com",
        "https://hub.daocloud.io"
    ]
```

![avatar](img/1.png)

修改完成后，点击右下角的应用并重启。在一下路径下，也可以直接修改文件。

- Linux: /etc/docker/daemon.json

- Windows: %USERPROFILE%\.docker\daemon.json 或 %programdata%\Docker\config\daemon.json

- MacOS: ~/.docker/daemon.json

作者：喵个咪
链接：https://juejin.cn/post/7165806699461378085
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# 使用docker安装redis

为什么是安装redis？前面不是说学习Elasticsearch？没办法,视频教程里面就是这样教的，而且本文的目的是为了学习Docker，redis还是Elasticsearch并不重要。

安装完docker后，再安装redis镜像只需要一个命令即可；

```shell
docker run -d -p 6379:6379 --name redis6.2.6 redis:6.2.6
```

![avatar](img/3.jpg)

- -d：这个命令表示后台运行

- -p：这个命令表示将docker中的6379端口映射到宿主机的6379端口

- --name：这个命令表示给镜像明明

- redis:6.2.6：这个表示拉取redis的镜像，版本号是6.2.6

想要了解docker的其他命令，可以在docker的官网文档中查找，文档地址：https://docs.docker.com/。比如要搜索run命令，如下图所示。

![avatar](img/2.jpg)

当命令执行成功，返回docker的控制台，查看容器和镜像情况。

![avatar](img/4.jpg)

redis已经通过docker容器运行起来了，如果本地安装了redis客户端，可以直接在本地访问，也可以在docker终端中访问redis。

- 本地方式

```shell
redis-cli  
127.0.0.1:6379> set docker_test '20230402'
OK
127.0.0.1:6379>
```

- 终端方式

![avatar](img/5.jpg)

![avatar](img/6.jpg)

# 安装Elasticsearch

```shell
# 拉取es镜像，版本为7.12.1
docker pull elasticsearch:7.14.1
# 查看已镜像
docker images
# 运行es镜像。-e表示设置环境变量，最后的字符串是本地已拉取的镜像id
docker run -d --name es -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" d090d5af83ca
```

下面是一段更复杂的脚本：

```shell
docker run -d \
	--name elasticsearch \
    -e "ES_JAVA_OPTS=-Xms512m -Xmx512m" \
    -e "discovery.type=single-node" \
    -v es-data:/usr/share/elasticsearch/data \
    -v es-plugins:/usr/share/elasticsearch/plugins \
    --privileged \
    --network itmentu-net \
    -p 9200:9200 \
    -p 9300:9300 \
elasticsearch:7.14.1
```

- -e "cluster.name=es-docker-cluster"：设置集群名称
- -e "http.host=0.0.0.0"：监听的地址，可以外网访问
- -e "ES_JAVA_OPTS=-Xms512m -Xmx512m"：内存大小
- -e "discovery.type=single-node"：非集群模式
- -v es-data:/usr/share/elasticsearch/data：挂载逻辑卷，绑定elasticsearch的数据目录
- -v es-logs:/usr/share/elasticsearch/logs：挂载逻辑卷，绑定elasticsearch的日志目录
- -v es-plugins:/usr/share/elasticsearch/plugins：挂载逻辑卷，绑定elasticsearch的插件目录
- --privileged：授予逻辑卷访问权
- --network itmentu-net ：加入一个名为itmentu-net的网络中
- -p 9200:9200：端口映射配置

在浏览器访问http://localhost:9200，返回如下json字符串，表示elasticsearch已安装成功。

```json
{
  "name" : "9046665f2b27",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "sxwz868ATxqm0VtZxDeHeQ",
  "version" : {
    "number" : "7.12.1",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "3186837139b9c6b6d23c3200870651f10d3343b7",
    "build_date" : "2021-04-20T20:56:39.040728659Z",
    "build_snapshot" : false,
    "lucene_version" : "8.8.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```
# 安装kibana

Kibana是一个开源的分析与可视化平台，设计出来用于和Elasticsearch一起使用的。你可以用kibana搜索、查看存放在Elasticsearch中的数据。Kibana与Elasticsearch的交互方式是各种不同的图表、表格、地图等，直观的展示数据，从而达到高级的数据分析与可视化的目的。

```shell
docker pull kibana:7.14.1
```

本来在安装elasticsearch时，安装的是7.12.1版本，但是由于我本地是M1芯片，暂时没有找到能支持M1芯片的kibana的7.12.1版本，想尝试一下是否可以es使用7.12.1，kinana使用7.14.1，但是发现不可以，启动kibana容器的时候会报错：This version of Kibana (v7.14.1) is incompatible with the following Elasticsearch nodes in your cluster: v7.12.1 @ 172.17.0.2:9200 (172.17.0.2)。最终把两个版本都调整为7.14.1。

```shell
docker run --name kibana -e ELASTICSEARCH_HOSTS=http://192.168.10.183:9200 -p 5601:5601 -d kibana:7.14.1
```
这里启动kibana的时候，如果ip写成localhost或127.0.0.1会有问题，可以直接改成本地的ip地址。

浏览器访问：http://localhost:5601/

![avatar](img/7.png)

如果需要频繁修改ip地址（换了个网络），可以参考下面的办法：

![avatar](img/8.png)


# 安装nacos

首先下载nacos的镜像。下载镜像时，注意镜像的cpu架构，比如我当前使用的是苹果的M1芯片，他属于arm架构。nacos的版本可以到docker镜像官网查看：https://hub.docker.com/。（点击进入nacos/nacos-server镜像，点击tags标签）

![avatar](img/9.png)

然后在本地拉取镜像，执行命令。其中最后冒号后面是要拉去的版本。--name表示容器名称，-d表示后台运行

```shell
docker run -p 8848:8848 --name nacos -d nacos/nacos-server:v2.2.2-slim
```

然后在本机电脑合适的路径下创建宿主机和docker内部的文件映射路径：

```shell
mkdir /Users/xxx/softwares/nacos/mydata/logs
mkdir /Users/xxx/softwares/nacos/mydata/conf
```

然后将docker中的文件拷贝到宿主机中。其中前面的路径表示宿主机中的路径。这一步启动nacos是为了将nacos里面的文件拷贝出到挂载目录中，这样我们就可以直接修改挂载目录中文件来映射到容器里面去了。

```shell
docker cp nacos:/home/nacos/logs/ /Users/xxx/softwares/nacos/mydata/logs
docker cp nacos:/home/nacos/conf/ /Users/xxx/softwares/nacos/mydata/conf
```

如上面提到的，这一步就是为了获得nacos的配置文件，此时nacos的容器已经可以销毁了，因为后面需要更为复杂的启动参数。

```shell
docker rm -f nacos
```

创建mysql数据库，数据库名称可以叫nacos_config，执行脚本在nacos的安装文件中可以找到。

![avatar](img/10.png)

修改nacos的配置文件，也就是刚刚从docker中拷贝出来的文件。主要是application.properties文件。再原有基础上增加下面的数据库配置。需要注意的是，如果数据库也是使用docker启动的，再次启动docker时可能会报数据源找不到的错误，是因为两个docker容器之间ip不同，这里的localhost是指nacos容器的ip，而不是数据库的ip。我这里把localhost改成了宿主机ip就可以了，其他方案可参考：https://blog.csdn.net/qq_45534014/article/details/121741552

```properties
spring.datasource.platform=mysql
db.num=1
db.url.0=jdbc:mysql://localhost:3306/nacos-config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=30000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user=root
db.password=root
```

最后重新创建nacos容器并启动：

```shell
docker run -d --name nacos -p 8848:8848  -p 9848:9848 -p 9849:9849 --privileged=true -e JVM_XMS=256m -e JVM_XMX=256m -e MODE=standalone -v /Users/xxx/softwares/nacos/mydata/logs:/home/nacos/logs -v /Users/xxx/softwares/nacos/mydata/conf:/home/nacos/conf --restart=always nacos/nacos-server:v2.2.2-slim
```

- docker run -d ： 启动容器 -d是后台启动并返回容器id的意思

- –name nacos ：为容器指定一个名称

- -p 8848:8848 -p 9848:9848 -p 9849:9849 ： 指定端口映射，注意这里的p不能大写，大写是随机端口映射

- –privileged=true ： 扩大容器内的权限，将容器内的权限变为root权限，不加的话就是普通用户权限，可能会出现cannot open directory

- -e JVM_XMS=256m ： 为jvm启动时分配的内存

- -e JVM_XMX=256m ： 为jvm运行过程中分配的最大内存

- -e MODE=standalone ： 使用 standalone模式（单机模式）,MODE值有cluster（集群）模式/standalone模式两种，MODE必须大写

- -v /mydata/nacos/logs/:/home/nacos/logs : 将容器的/home/nacos/logs目录挂载到 /mydata/nacos/logs

- -v /mydata/nacos/conf/:/home/nacos/conf/： 将容器的/home/nacos/conf目录挂载到 /mydata/nacos/conf

- –restart=always ：重启docker时，自动启动相关容器

最后在网页访问nacos：http://ip:8848/nacos/index.html

![avatar](img/11.png)

![avatar](img/12.png)







