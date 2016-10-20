FROM ubuntu:14.04
MAINTAINER "abel" abe1ge@github.com

RUN sudo apt-get update
RUN sudo apt-get install default-jre -y
RUN sudo apt-get install default-jdk -y
RUN sudo apt-get install wget -y
RUN sudo apt-get update

WORKDIR /opt/
RUN wget www.sonatype.org/downloads/nexus-2.12.0-01-bundle.tar.gz

CMD echo "finished"

