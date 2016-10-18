FROM ubuntu:14.04
MAINTAINER abel "abe1ge@github.git"

# Update apt-get
RUN apt-get update

# install software 
RUN apt-get install -y git
RUN apt-get install -y vim
RUN apt-get install -y default-jre default-jdk
RUN apt-get install -y maven

# git clone
WORKDIR /opt/
RUN git clone git://github.com/dasanjos/java-WebServer

# config
WORKDIR /opt/java-WebServer/
RUN mvn clean package
WORKDIR target

#run this command once the container runs 
ENTRYPOINT  java -jar java-WebServer-0.1-jar-with-dependencies.jar 
