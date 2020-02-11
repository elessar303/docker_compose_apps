FROM mysql:5.7

# instalamos paquetes
RUN apt-get update && apt-get install nano

ADD ./config/mysql/my.cnf /etc/mysql/conf.d/my.cnf

RUN chmod 644 /etc/mysql/conf.d/my.cnf