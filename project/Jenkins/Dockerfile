FROM ubuntu:14.04
MAINTAINER "abel" abe1ge@github.com

RUN apt-get update

RUN apt-get install wget -y

RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -

RUN sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

RUN sudo apt-get update -y

RUN sudo apt-get install jenkins -y

ENTRYPOINT service jenkins start && bash 
