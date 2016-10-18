FROM ubuntu:14.04
MAINTAINER abel "abe1ge@githob.git"

# Update apt-get
RUN apt-get update

# install softwar
RUN apt-get install -y git
RUN apt-get install -y vim
 
# installing Java and maven
RUN apt-get install -y default-jre default-jdk
RUN apt-get install -y maven

# git clone
WORKDIR /opt/

RUN git clone git://github.com/dasanjos/java-WebServer

WORKDIR /opt/java-WebServer/

RUN mvn clean package

WORKDIR target
ENTRYPOINT  java -jar java-WebServer-0.1-jar-with-dependencies.jar 
