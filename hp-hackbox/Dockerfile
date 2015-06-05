FROM ubuntu:trusty
MAINTAINER Clark Laughlin <clark at laughlins dot org>

ENV DEBIAN_FRONTEND noninteractive


RUN apt-get update && apt-get -y upgrade
RUN apt-get install --no-install-recommends -y language-pack-en
RUN apt-get install --no-install-recommends -y tmux unzip zip elinks git vim build-essential man
RUN apt-get clean

ENV http_proxy http://web-proxy.houston.hp.com:8080

RUN echo 'Acquire::http::Proxy "http://web-proxy.houston.hp.com:8080";' >> /etc/apt/apt.conf
RUN echo "export http_proxy=$http_proxy" >> /root/.bashrc && \
  echo "export https_proxy=$http_proxy" >> /root/.bashrc && \
  echo "export HTTP_PROXY=$http_proxy" >> /root/.bashrc && \
  echo "export HTTPS_PROXY=$http_proxy" >> /root/.bashrc
