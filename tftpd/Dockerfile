FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y tftpd-hpa

RUN mkdir /srv/tftp
VOLUME /srv/tftp

EXPOSE 69
CMD /usr/sbin/in.tftpd --foreground --user tftp --address 0.0.0.0:69 --secure /srv/tftp

