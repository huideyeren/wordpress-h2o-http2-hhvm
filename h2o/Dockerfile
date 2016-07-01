FROM ubuntu:latest

MAINTAINER Takakura Yusuke (takakura.yusuke@gmail.com)

LABEL Description = "H2O Web Server"

# Install Package

RUN apt-get -y update
RUN apt-get -y upgrade

RUN apt-get install -y libuv-dev libyaml-dev libssl-dev cmake git build-essential

# Build H2O

WORKDIR /tmp
RUN git clone https://github.com/h2o/h2o.git
WORKDIR /tmp/h2o
RUN git submodule update --init --recursive
RUN cmake .
RUN make h2o
RUN mv /tmp/h2o/h2o /usr/sbin/h2o
RUN mkdir /etc/h2o
RUN mkdir /srv/wordpress
WORKDIR /etc/h2o
ADD h2o.conf h2o.conf

RUN rm -rf /tmp/h2o

WORKDIR /usr/local/share/h2o

RUN openssl genrsa -out server.key 4096
RUN openssl req -new -batch -key server.key -out server.csr
RUN openssl x509 -req -days 3650 -in server.csr -signkey server.key -out server.crt
RUN ln -s /etc/ssl/certs/ca-certificates.crt ca-bundle.crt
COPY ./fetch-ocsp-response fetch-ocsp-response

CMD h2o -c /etc/h2o/h2o.conf

VOLUME ["/etc/h2o", "/srv/wordpress"]
