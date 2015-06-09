FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y dnsmasq iptables

RUN wget --no-check-certificate https://raw.githubusercontent.com/jpetazzo/pipework/master/pipework
RUN chmod +x pipework

VOLUME /etc/dnsmasq.d

# DNS: TCP/UDP port 53
EXPOSE 53

# DHCP: UDP ports 67 (server) and 68 (client)
EXPOSE 67
EXPOSE 68

# TFTP: UDP port 69
EXPOSE 69

CMD \
    echo Setting up iptables... &&\
    iptables -t nat -A POSTROUTING -j MASQUERADE &&\
    echo Waiting for pipework to give us the eth1 interface... &&\
    /pipework --wait &&\
    myIP=$(ip addr show dev eth1 | awk -F '[ /]+' '/global/ {print $3}') &&\
    mySUBNET=$(echo $myIP | cut -d '.' -f 1,2,3) &&\
    echo Starting DHCP+TFTP server...&&\
    /usr/sbin/dnsmasq --interface=eth1 --keep-in-foreground --log-facility=- --user=root --dhcp-authoritative --conf-dir=/etc/dnsmasq.d --enable-tftp --tftp-root=/srv/tftp
