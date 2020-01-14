# chapter_02: 搭建canal-admin容器
![canal-docker-demo-搭建](/res/p_00.png)

canal-admin服务本身是依赖数据库服务。在canal-admin启动过程中发现容器本身会启动MySQL服务，数据库名：canal_manager，而且默认数据库账号是canal账号（后续canal-server默认账号也是canal）。为了有更好的辨识度，习惯直接在账号名称上做区分。

出于以上的原因，重新打了本地canal-admin镜像：
* 替换默认canal账号为canal-admin账号
* 调整启动脚本，关闭加载MySQL服务


## dev-mysql容器的作用
1. 由于重新打包的canal-admin镜像，关闭了默认自带的MySQL，所以需要将canal_manager数据库导入到 dev-mysql容器服务。
2. dev-mysql同时充当canal-server的一个instance。

## canal_manager数据库导入dev-mysql容器
1. 通过官方canal-admin镜像创建一个默认容器。通过exec指令连进容器，导出canal_manager。(默认自带的数据库root账号密码为Hello1234，可以在初始化脚本中查到)
2. [canal-admin release包v1.1.4](https://github.com/alibaba/canal/releases/download/canal-1.1.4/canal.admin-1.1.4.tar.gz)，解压后`conf/canal_manager.sql`文件。


## 重新打包canal-admin镜像
```sh
# Dockerfile 所在目录
docker build -t personal/canal-admin:v1.1.4 .

docker run --name=canal-admin \
    -d \
    -it \
    --net=container:dev \
    -e canal.admin.manager=127.0.0.1:8089 \
    -e canal.admin.port=11110 \
    -e canal.admin.user=admin \
    -e canal.admin.passwd=4ACFE3202A5FF5CF467898FC58AAB1D615029441 \
    -m 4096m \
    personal/canal-admin:v1.1.4
```

在数据库授权正常的情况下，本机访问http://localhost:8089，登录canal-admin后台。(账号/密码：admin/123456)
