FROM ubuntu
MAINTAINER abel <abe1ge@github.com>

RUN  apt-get update
RUN apt-get install zabbix-agent -y

RUN sed -i -e 's/=127.0.0.1/=52.212.191.25/g' /etc/zabbix/zabbix_agentd.conf

ENTRYPOINT  service zabbix-agent start && bash
