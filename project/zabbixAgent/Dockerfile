FROM ubuntu:14.04
MAINTAINER abel <abe1ge@github.com>

RUN  apt-get update
RUN apt-get install zabbix-agent -y

RUN sed -i -e 's/Server=127.0.0.1/Server=52.212.198.158/g' /etc/zabbix/zabbix_agentd.conf
RUN sed -i -e 's/ServerActive=127.0.0.1/ServerActive=52.212.198.158/g' /etc/zabbix/zabbix_agentd.conf

ENTRYPOINT service zabbix-agent start && bash


