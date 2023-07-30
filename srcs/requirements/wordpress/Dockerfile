FROM debian:bullseye

EXPOSE 9000

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install php7.3 php-fpm wget php7.3-mysql curl && \
        apt install -y dumb-init

RUN mkdir -p /var/www
RUN wget https://wordpress.org/latest.tar.gz
RUN tar -xvf latest.tar.gz && mv /wordpress/* /var/www
RUN chown -R www-data:www-data /var/www
RUN rm -r /wordpress latest.tar.gz

COPY ./conf/www.conf /etc/php/7.3/fpm/pool.d/
COPY ./conf/wp-config.php /var/www/
COPY ./tools/entry.sh /tmp/

RUN chmod +x /tmp/entry.sh


ENTRYPOINT [ "dumb-init", "--", "/tmp/entry.sh" ]
