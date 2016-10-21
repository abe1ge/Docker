ntn: 52.212.124.65
academy
abel: 52.31.46.88

sudo usermod -aG docker ubuntu

sudo docker run -d -i -t ubuntu bash

sudo docker run -d -p 8080:8080 -ti  ubuntu bash


This project required me, in a team, to use Puppet and Puppet Enterprise to construct an entirely automated system for installing and configuring a continuous integration pipeline. The team managed the project by utilising the SCRUM framework, using Git for version control, and using JIRA to monitor progress. By using vagrant, I set up a number of servers that would automatically communicate with a puppet master and carry out puppet runs at scheduled intervals. The generation and signing of the certificates by the master was all fully automated. 

I was tasked with creating an environment that would launch Jenkins, Jira, Nexus, Zabbix and UrbanCode-Deploy using Docker. By using the Dockerfile convention, I created containers that would deploy each tool as specified. Through the use of docker compose I was able to deploy all the containers at once. I also used docker swarm to manage the containers. 

sudo vim atlassian-jira/WEB-INF/cl   asses/jira-application.properties

jira.home =/var/jira 

docker rmi the_image
However, if you need to remove multiple you could use:

Remove all images

  docker rmi $(docker images -qf "dangling=true")
  docker rmi $(docker images -q)
Kill containers and remove them:

  docker rm $(docker kill $(docker ps -aq))
Note: Replace kill with stop for graceful shutdown

Remove all images except "my-image"

You could use grep to remove all except my-image and ubuntu

  docker rmi $(docker images | grep -v 'ubuntu\|my-image' | awk {'print $3'})
