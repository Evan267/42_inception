FROM debian:buster

RUN apt update -y \
	&& apt upgrade -y

RUN apt-get -y install wget \
	php7.3 \
	php-fpm \
	php-mysql \
	mariadb-client

RUN wget https://fr.wordpress.org/latest-fr_FR.tar.gz -P /var/www

RUN cd /var/www && tar -xzf latest-fr_FR.tar.gz && rm latest-fr_FR.tar.gz

RUN chown -R root:root /var/www/wordpress

COPY conf/www.conf /etc/php/7.3/fpm/pool.d/www.conf

RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar

RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

COPY conf/auto-config.sh /bin/auto-config.sh

RUN chmod +x /bin/auto-config.sh

ENTRYPOINT ["bin/auto-config.sh"]

RUN mkdir /run/php
