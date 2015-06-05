FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y dnsmasq

VOLUME /etc/dnsmasq.d

# DNS: TCP/UDP port 53
EXPOSE 53

# DHCP: UDP ports 67 (server) and 68 (client)
EXPOSE 67
EXPOSE 68

# TFTP: UDP port 69
EXPOSE 69

CMD /usr/sbin/dnsmasq --keep-in-foreground --log-facility=- --dhcp-authoritative --conf-dir=/etc/dnsmasq.d --enable-tftp --tftp-root=/srv/tftp
