FROM debian:bullseye

EXPOSE 9000

RUN apt-get update && \
    apt-get -y install dumb-init && \
    apt-get -y upgrade && \
    apt-get -y install php7.4 php-fpm wget php7.4-mysql curl

RUN mkdir -p /var/www
RUN wget https://wordpress.org/latest.tar.gz
RUN tar -xvf latest.tar.gz && mv /wordpress/* /var/www
RUN chown -R www-data:www-data /var/www
RUN rm -r /wordpress latest.tar.gz

COPY ./conf/www.conf /etc/php/7.4/fpm/pool.d/
COPY ./conf/wp-config.php /var/www/
COPY ./tools/entry.sh /tmp/

RUN chmod +x /tmp/entry.sh


ENTRYPOINT [ "dumb-init", "--", "/tmp/entry.sh" ]
