# canal_demo
开始学习canal教程
[alibaba / canal](https://github.com/alibaba/canal) 是alibaba开源的基于MySQL数据库增量日志（binary log）解析，提供数据增量消费。

开源最新的版本是v1.1.4，最大的特色是提供了canal-admin，主要提供集群管理，server管理，instance管理。

由于开始学习，且涉及到的开源组建较多，做个基于docker个人开发环境搭建整套canal服务，并将增量消息到MQ。

![canal-docker-demo-搭建](/res/p_00.png)

![canal-docker-demo-搭建](/res/p_01.gif)


# 主要涉及docker镜像

* [canal/canal-server:v1.1.4](https://hub.docker.com/r/canal/canal-server)
* [canal/canal-admin:v1.1.4](https://hub.docker.com/r/canal/canal-admin)
* [mysql:5.7](https://hub.docker.com/_/mysql)
* [ches/kafka:latest](https://hub.docker.com/r/ches/kafka)
* [zookeeper:3.4](https://hub.docker.com/_/zookeeper)


# 准备工作
个人的开发环境是macOS。(理论上linux和windows同样)
安装好Docker服务，并且对docker命令有一定了解。
推荐[jesseduffield / lazydocker](https://github.com/jesseduffield/lazydocker)，一个docker的命令行可视化工具，对搭建调试是观察日志比较便利。




