FROM ubuntu:16.04
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      wget tar build-essential gcc bison flex autoconf libxml2-dev \
 && cd /tmp \
 && wget -nv --no-check-certificate https://github.com/php/php-src/archive/php-7.1.1.tar.gz \
 && tar -xf php-7.1.1.tar.gz \
 && rm *.tar.gz \
 && mv php* /opt/php \
 && cd /opt/php \
 && ./buildconf --force \
 && ./configure \
 && make -j8 \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
WORKDIR /opt/php
COPY . /inputs
