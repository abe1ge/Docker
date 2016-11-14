
FROM ubuntu
MAINTAINER "abel" abe1ge@github.com

RUN apt-get update

#install dependencies
RUN apt-get install wget maven -y

#installing the latest  jdk and jre
RUN apt install -y openjdk-8-jre-headless
RUN export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

#getting the key
RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | apt-key add -

#allow jenkins to be installed
RUN sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

RUN apt-get update -y

RUN apt-get install jenkins -y

ENTRYPOINT service jenkins start && bash
