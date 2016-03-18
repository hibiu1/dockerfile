FROM ubuntu:15.10
MAINTAINER hibiu1

# noninteractive mode
# 文字化け対策
# http://qiita.com/tailak/items/77b90a4df07e4f6a1fc2
ENV \
  DEBIAN_FRONTEND=noninteractive

RUN \
  echo "Asia/Tokyo" > /etc/timezone \
  locale-gen en_US.UTF-8

RUN \
  apt-get update && \
  apt-get install -y pppoe

# PPPoE configuration
# DNS server1,2 : 200.0.0.101, 200.0.0.102
# MTU : 1454 bytes
# proxyarp
RUN \
  sed -i -e "s/# ms-dns 192.168.1.1/ms-dns 200.0.0.101/" /etc/ppp/options && \
  sed -i -e "s/# ms-dns 192.168.1.2/ms-dns 200.0.0.102/" /etc/ppp/options && \
  sed -i -e "s/#mtu <n>/mtu 1454/" /etc/ppp/options && \
  sed -i -e "s/#proxyarp/proxyarp/" /etc/ppp/options


# PPPoE user, password : pppoe-client, pppoe-client
# PPPoE Clinet IP : 200.0.0.240
RUN \
  echo "pppoe-client * \"pppoe-client\" 200.0.0.240" >> /etc/ppp/pap-secrets

RUN \
 apt-get clean
