# chapter_03: 搭建canser-server容器
![canal-docker-demo-搭建](/res/p_00.png)

canal-server镜像默认severMode=tcp配置，所以这里也重新打了镜像，调整配置serverMode=kafka，修改MQ服务地址为后面使用的kafka地址。


```sh
# Dockerfile 所在目录
docker build -t personal/canal-server:v1.1.4 .


docker run --name=canal-server \
    --rm \
    -d \
    -it \
    --net=container:dev \
    -e canal.instance.master.address=127.0.0.1:3306 \
    -e canal.instance.dbUsername=canal -e canal.instance.dbPassword=canal \
    -e canal.instance.connectionCharset=UTF-8 \
    -e canal.instance.tsdb.enable=true \
    -e canal.instance.gtidon=false \
    -e canal.instance.filter.regex=.*\..* \
    -m 4096m \
    personal/canal-server:v1.1.4
```

canal-server还支持指定canal-admin服务地址启动，这样默认server信息就会自动添加到admin系统。

默认启动后，会有一个名为example增量消息监听（dev-mysql），并将消息投递到kafka（topic为example）
