FROM ubuntu:14.04
MAINTAINER abel <abe1ge@github.com>
USER root
RUN echo "deb http://ppa.launchpad.net/tbfr/zabbix/ubuntu precise main" >> /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/tbfr/zabbix/ubuntu precise main" >> /etc/apt/sources.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C407E17D5F76A32B
RUN apt-get update

#RUN debconf-set-selections <<< 'mysql-server mysql-server/root_password password zabbix'
#RUN  debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password zabbix'

RUN DEBIAN_FRONTEND=noninteractive apt-get install zabbix-server-mysql php5-mysql zabbix-frontend-php

#RUN sed -i "/#DBPassword=''/c\DBPassword=zabbix" /etc/zabbix/zabbix_server.conf

WORKDIR /usr/share/zabbix-server-mysql/
RUN gunzip *.gz

RUN mysql service start 
&& mysql -u root -e "create user 'zabbix'@'localhost' identified by '';\
&& mysql -u root -e "create database zabbix;\
&& mysql -u root -e "grant all privileges on zabbix.* to 'zabbix'@'localhost';"\
&& mysql -u root -e  "flush privileges;"\
&& mysql -u zabbix  zabbix < schema.sql\
&& mysql -u zabbix  zabbix < data.sql

RUN sed -i "/post_max_size =/c\post_max_size = 16M" /etc/php5/apache2/php.ini
RUN sed -i "/max_execution_time =/c\max_execution_time = 300" /etc/php5/php.ini
RUN sed -i "/max_input_time =/c\max_input_time = 300" /etc/php5/php.ini
RUN sed -i "/;date.timezone =/c\date.timezone = UTC" /etc/php5/php.ini

RUN cp /usr/share/doc/zabbix-frontend-php/examples/zabbix.conf.php.example /etc/zabbix/zabbix.conf.php

ENTRYPOINT service zabbix-server start && bash


