FROM ubuntu:14.04
Maintainer "abel" abe1ge@github.com

RUN sudo apt-get update 

#installing dependencies
RUN sudo apt-get install wget -y
RUN apt-get install default-jre -y
RUN apt-get install default-jdk -y


#download jira
WORKDIR /opt/
RUN sudo wget https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-6.4.2.tar.gz

# unzip jira
RUN sudo tar -xvzf atlassian-jira-6.4.2.tar.gz

#configuration
RUN sudo mkdir /var/jira

WORKDIR /opt/atlassian-jira-6.4.2-standalone/atlassian-jira/WEB-INF/classes/
RUN sed -i '/jira.home =/c\jira.home = \/var\/jira' jira-application.properties

WORKDIR /opt/atlassian-jira-6.4.2-standalone/bin/


ENTRYPOINT ./start-jira.sh && bash

