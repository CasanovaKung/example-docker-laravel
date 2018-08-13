FROM mysql:5.7.22

LABEL maintrainer="Jakkrapan Wongchan<casanovakung@windowslive.com>"

ADD ./conf.d/charset.cnf /etc/mysql/conf.d/charset.cnf

EXPOSE 3306
CMD ["mysqld"]
