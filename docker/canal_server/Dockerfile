FROM canal/canal-server:v1.1.4

# 更改默认serverMode=kafka
RUN sed -i -e "s/canal.serverMode = tcp/canal.serverMode = kafka/" /home/admin/canal-server/conf/canal.properties

# 更改MQserver为 kafka地址
RUN sed -i -e "s/canal.mq.servers = 127.0.0.1:6667/canal.mq.servers = 127.0.0.1:9092/" /home/admin/canal-server/conf/canal.properties
