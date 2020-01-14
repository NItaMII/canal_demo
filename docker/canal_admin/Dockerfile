FROM canal/canal-admin:v1.1.4

# Delete self-mysql
RUN sed -i -e 's/^[ ]*start_mysql$/:/g' /home/admin/app.sh

RUN sed -i -e 's/^stop_mysql$//g' /home/admin/app.sh

# 更改自定canal_manager数据库账号和canal-server默认账号做区分
RUN sed -i -e 's/username: canal$/username: canal_admin/g' /home/admin/canal-admin/conf/application.yml

RUN sed -i -e 's/password: canal$/password: canal_admin/g' /home/admin/canal-admin/conf/application.yml
