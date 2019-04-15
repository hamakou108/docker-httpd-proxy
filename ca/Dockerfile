FROM centos:7
LABEL maintainer="hamakou108 <kosuke1602177mteitm19@gmail.com>"

RUN yum -y update \
    && yum -y install openssl \
    && yum clean all \
    && rm -rf /var/cache/yum/*

WORKDIR /etc/pki/CA
COPY CA .
COPY openssl.cnf .
RUN echo 00 > ./serial

CMD ["/bin/bash"]

