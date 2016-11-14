FROM ubuntu:14.04
MAINTAINER "abel" abe1ge@github.com

RUN apt-get update

#install dependencies 
RUN apt-get install wget maven -y

#installing java 1.8.0_45
WORKDIR /opt/
RUN sudo wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jdk-8u45-linux-x64.tar.gz"
RUN sudo tar -zxvf jdk-8u45-linux-x64.tar.gz
WORKDIR /opt/jdk1.8.0_45/
RUN update-alternatives --install /usr/bin/java java /opt/jdk1.8.0_45/bin/java 100
RUN update-alternatives --install /usr/bin/javac javac /opt/jdk1.8.0_45/bin/javac 100

RUN export JAVA_HOME=/opt/jdk1.8.0_45/


#getting the key
RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -

#allow jenkins to be installed
RUN sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

RUN sudo apt-get update -y

RUN sudo apt-get install jenkins -y

ENTRYPOINT service jenkins start && bash 
