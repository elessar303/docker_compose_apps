FROM mysql:5.7

# instalamos paquetes
RUN apt-get update && apt-get install nano

ADD ./config/mysql/my.cnf /etc/mysql/conf.d/my.cnf

ADD ./config/mysql/error.log /var/log/mysql/error.log

ADD ./config/mysql/general_log.log /var/log/mysql/general_log.log

ADD ./config/mysql/mysql_slow.log /var/log/mysql/mysql_slow.log

RUN chmod 644 /etc/mysql/conf.d/my.cnf

RUN chown -R mysql.mysql /var/log/mysql

RUN chmod 777 /var/log/mysql/general_log.log

RUN chmod 777 /var/log/mysql/error.log

EXPOSE 3306