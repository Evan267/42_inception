FROM debian:buster

RUN apt update -y \
	&& apt upgrade -y \
	&& apt install nginx -y \
	&& apt install vim -y \
	&& apt install curl -y \
	&& apt install openssl -y

RUN mkdir -p etc/nginx/ssl

RUN openssl req -x509 -nodes -out /etc/nginx/ssl/inception.crt -keyout /etc/nginx/ssl/inception.key -subj "/C=FR/ST=HR/L=Mulhouse/O=42/OU=42/CN=eberger.42.fr/UID=eberger"

RUN chmod 755 /var/www/html

RUN chown -R www-data:www-data /var/www/html

COPY conf/nginx.conf /etc/nginx/nginx.conf

CMD [ "nginx", "-g", "daemon off;" ]
