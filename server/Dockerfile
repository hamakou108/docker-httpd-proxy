FROM httpd:2.4
LABEL maintainer="hamakou108 <kosuke1602177mteitm19@gmail.com>"

RUN apt-get update \
    && apt-get install -y openssl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
COPY openssl.cnf /etc/ssl/

COPY httpd.conf ./conf/
COPY httpd-ssl.conf ./conf/extra/
COPY server-key-dec.pem ./conf/ssl/
COPY server-cert-dec.pem ./conf/ssl/
COPY cacert.pem ./conf/ssl/

CMD ["httpd-foreground"]

