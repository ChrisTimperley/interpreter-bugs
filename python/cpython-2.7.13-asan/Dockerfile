FROM ubuntu:18.04
ENV ASAN_OPTIONS "detect_leaks=0:symbolize=1:coverage=1"
RUN sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
      ca-certificates wget tar build-essential gcc bison flex autoconf libxml2-dev \
      clang-4.0 clang++-4.0 clang-tools-4.0 \
 && DEBIAN_FRONTEND=noninteractive apt-get build-dep -y python2.7 \
 && cd /tmp \
 && wget -nv https://github.com/python/cpython/archive/v2.7.13.tar.gz \
 && tar -xf *.tar.gz \
 && rm *.tar.gz \
 && mv /tmp/cpython-2.7.13 /opt/python \
 && cd /opt/python \
 && ./configure \
      CC="clang-4.0" \
      CXX="clang++-4.0" \
      CFLAGS="-g -fsanitize=address -fno-omit-frame-pointer -O0 -fsanitize-coverage=bb" \
      CPPFLAGS="-fsanitize=address -fno-omit-frame-pointer -O0 -fsanitize-coverage=bb" \
      LDFLAGS="-fsanitize=address" \
 && make -j8 \
 && make install \
 && rm -rf /tmp/* \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
WORKDIR /opt/python
COPY . /inputs
