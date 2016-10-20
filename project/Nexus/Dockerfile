FROM ubuntu:14.04
MAINTAINER "abel" abe1ge@github.com

RUN sudo apt-get update
RUN sudo apt-get install wget -y
RUN sudo apt-get install vim
RUN sudo apt-get install maven
RUN sudo apt-get update

#installing java 1.8.0_45
RUN sudo wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jdk-8u45-linux-x64.tar.gz"
RUN sudo tar -zxvf jdk-8u45-linux-x64.tar.gz
WORKDIR /opt/jdk1.8.0_45/
RUN update-alternatives --install /usr/bin/java java /opt/jdk1.8.0_45/bin/java 100
RUN update-alternatives --install /usr/bin/javac javac /opt/java/jdk1.8.0_45/bin/javac 100

WORKDIR /opt/
RUN wget http://download.sonatype.com/nexus/3/nexus-3.0.2-02-unix.tar.gz
RUN sudo tar -zxvf nexus-3.0.2-02-unix.tar.gz
RUN sudo ln -s nexus-3.0.2-02 nexus
WORKDIR /
RUN sudo ln -s /opt/nexus/bin/nexus /etc/init.d/nexus

WORKDIR /etc/init.d/
RUN sudo update-rc.d nexus defaults

ENTRYPOINT sudo service nexus start

