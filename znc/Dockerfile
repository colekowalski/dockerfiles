FROM debian:jessie

MAINTAINER Cole Kowalski <cole@northernbloc.org>

ENV ZNC_VERSION 1.6.3

RUN useradd -M -r znc

RUN apt-get update \
 && apt-get install -y curl python3 libicu52 zlib1g \
 && curl -sSL https://bootstrap.pypa.io/get-pip.py | python3

RUN DEPS='build-essential \
          pkg-config \
          python3-dev \
          libicu-dev \
          libssl-dev \
          zlib1g-dev' \
 && apt-get -y install ${DEPS} \
 && curl -sSL "http://znc.in/releases/znc-${ZNC_VERSION}.tar.gz" -o /usr/src/znc.tar.gz \
 && tar -xzf /usr/src/znc.tar.gz -C /usr/src/ \
 && cd /usr/src/znc-${ZNC_VERSION} \
 && ./configure --enable-python \
 && make \
 && make install \
 && rm -rf /usr/src/* \
 && apt-get purge -y --auto-remove $DEPS \
 && rm -rf /var/lib/apt/lists

USER znc

ENTRYPOINT ["/usr/local/bin/znc"]
