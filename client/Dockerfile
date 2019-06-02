FROM centos:7
LABEL maintainer="hamakou108 <kosuke1602177mteitm19@gmail.com>"

RUN yum -y update \
    && yum -y install openssl \
    && yum clean all \
    && rm -rf /var/cache/yum/*
COPY openssl.cnf /etc/pki/tls/

WORKDIR /opt
COPY client-key-dec.pem ./ssl/
COPY client-cert-dec.pem ./ssl/
COPY cacert.pem ./ssl/

CMD ["/bin/bash"]

