# chapter_01: 搭建dev-mysql容器
![canal-docker-demo-搭建](/res/p_00.png)

由于MySQL是数据存储服务，所以单独将数据目录，配置目录等
单独挂的宿主机本地。
```sh
LOCAL_MYSQL_PATH=~/docker/mysql5.7
docker run --name dev-mysql \
    --rm \
    -d \
    --net=container:dev \
    -v $LOCAL_MYSQL_PATH/etc:/etc/mysql/conf.d \
    -v $LOCAL_MYSQL_PATH/data:/var/lib/mysql \
    -v $LOCAL_MYSQL_PATH/run:/var/run/mysqld \
    -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:5.7
```

`--net=container:dev`: 表示该容器共用dev容器的网络。

前面提到dev宿主容器暴露了3306端口，这样在数据机器上也能访问dev-mysql容器提供的MySQL服务。

# 关于MySQL配置
由于后续使用canal，MySQL服务需要打开bin_log，并且格式设置为Row模式。
以上可以通过修改刚刚挂出来的配置目录，调整后重启容器即可。


`--rm` 在没有特殊情况下，个人开发环境尽量保证容器无状态是一个好的选择

