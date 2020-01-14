# chapter_00: 搭建dev宿主容器
![canal-docker-demo-搭建](/res/p_00.png)

由于是macOS，Docker不支持host网络模式。所以搭建宿主容器dev，对外（宿主机）暴露端口，对内集成所有服务容器。应该算有点类似K8S中pod的概念。
宿主容器dev, 这里选的是centos镜像，可以换成其他的基础系统镜像。
```sh
docker run --name dev \
    --rm \
    -it \
    -d \
    -p 3306:3306 \
    -p 8089:8089\
    centos bash
```

对外暴露3306（MySQL服务），8089（canal-admin）。



# 整体效果展示

