FROM anapsix/alpine-java

MAINTAINER HuChangwei <hcwzqmail@gmail.com>

WORKDIR /app

VOLUME /app

RUN apk add --update mysql mysql-client && rm -f /var/cache/apk/*

COPY my.cnf /etc/mysql/my.cnf

COPY startMysql.sh /app/startMysql.sh


EXPOSE 3306
