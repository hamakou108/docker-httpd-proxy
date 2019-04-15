FROM httpd:2.4
LABEL maintainer="hamakou108 <kosuke1602177mteitm19@gmail.com>"

RUN apt-get update \
    && apt-get install -y openssl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
COPY openssl.cnf /etc/ssl/

COPY httpd.conf ./conf/
COPY httpd-ssl.conf ./conf/extra/
COPY server.key ./conf/
COPY server.crt ./conf/
COPY cacert.pem ./conf/

CMD ["httpd-foreground"]

