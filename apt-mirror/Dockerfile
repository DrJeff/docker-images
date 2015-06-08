FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y lighttpd apt-mirror

ADD miror.list /etc/apt/mirror.list
ADD lighttpd.conf /etc/lighttpd/lighttpd.conf

VOLUME /var/www
EXPOSE 80

RUN apt-mirror
RUN adduser www-data -G www-data -H -s /bin/false -D

ENTRYPOINT ["lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
