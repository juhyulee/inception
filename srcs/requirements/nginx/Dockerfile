FROM    debian:bullseye

EXPOSE 443

RUN     apt-get update && \
        apt-get -y upgrade && \
        apt-get -y install nginx openssl


COPY    ./conf/default /etc/nginx/sites-available

RUN     openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/juhyulee.key -out /etc/ssl/juhyulee.crt \
        -subj "/C=KR/ST=Seoul/L=Seoul/O=42Seoul/OU=juhyulee"

RUN     chmod 700 /etc/ssl/juhyulee.crt
RUN     chmod 700 /etc/ssl/juhyulee.key


ENTRYPOINT ["nginx", "-g", "daemon off;"]
