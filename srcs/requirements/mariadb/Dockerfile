FROM debian:buster

RUN apt update -y \
    && apt upgrade -y \
    && apt-get install mariadb-server -y

COPY conf/50-server.cnf /etc/mysql/mariadb.conf.d/50-server.cnf

RUN mysql -e "CREATE DATABASE IF NOT EXISTS \`${MYSQL_DATABASE}\`;"

RUN mysql -e "CREATE USER IF NOT EXISTS \`${MYSQL_USER}\`@'localhost' IDENTIFIED BY '${MYSQL_PASSWORD}';"

RUN mysql -e "GRANT ALL PRIVILEGS ON \`${MYSQL_DATABASE}\`.* TO \`${MYSQL_USER}\`@'%' IDENTIFIED BY '${MYSQL_PASSWORD}';"

RUN mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED BY '${MYSQL_ROOT_PASSWORD}';"

RUN mysql -e "FLUSH PRIVILEGES;"

RUN mysqladmin -u root -p$MYSQL_ROOT_PASSWORD shutdown

RUN exec mysqld_safe
