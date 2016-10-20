FROM ubuntu:14.04

RUN sudo apt-get update -y

RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -

RUN sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

RUN sudo apt-get update

RUN sudo apt-get install jenkins

 
