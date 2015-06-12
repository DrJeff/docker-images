FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y isc-dhcp-server wget

RUN wget --no-check-certificate https://raw.githubusercontent.com/jpetazzo/pipework/master/pipework
RUN chmod +x pipework
RUN mv pipework /usr/bin/.

RUN mkdir -p /srv/dhcpd
VOLUME /srv/dhcpd

CMD \
    echo Waiting for pipework to give us the eth1 interface... &&\
    pipework --wait -i eth1 &&\
    myIP=$(ip addr show dev eth1 | awk -F '[ /]+' '/global/ {print $3}') &&\
    mySUBNET=$(echo $myIP | cut -d '.' -f 1,2,3) &&\
    echo "Starting DHCP server (ip=${myIP}, subnet=${mySUBNET})..."&&\
    dhcpd -f eth1 -cf /srv/dhcpd/dhcpd.conf -lf /srv/dhcpd/dhcpd.leases
