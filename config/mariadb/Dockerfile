FROM mariadb:10.7
# instalamos paquetes
RUN apt-get update && apt-get install nano

ADD ./config/mysql/my.cnf /etc/mysql/conf.d/my.cnf

RUN chmod 644 /etc/mysql/conf.d/my.cnf

RUN chown -R mysql.mysql /var/log/mysql

EXPOSE 3306