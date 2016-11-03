ntn: 52.212.124.65
academy
abel: 52.210.229.150

See what is using a specfic port

	sudo lsof -i :8080
<b> add user to rute </b>
	
	sudo usermod -aG docker ubuntu
	
<h3> uninstalling files </h3>
a specific app:

	apt-get remove <app>
find all installed apps downloaded after a certin date:

	grep "2016-11-02.*.install " /var/log/dpkg.log | awk '{ print $4 }' | cut -d: -f1
removing them :

	sudo apt-get purge app1 app2
	
<h3> searching for a word in a document </h3>

	grep installed /var/log/dpkg.log
	grep 'word' filename
	grep 'word' file1 file2 file3
	grep 'string1 string2'  filename
	cat otherfile | grep 'something'
	command | grep 'something'
	command option1 | grep 'data'
	grep --color 'data' fileName

<h1> Docker command </h1>

	sudo docker run -d -i -t ubuntu bash

	sudo docker run -d -p 8080:8080 -ti  ubuntu bash

This project required me, in a team, to use Puppet and Puppet Enterprise to construct an entirely automated system for installing and configuring a continuous integration pipeline. The team managed the project by utilising the SCRUM framework, using Git for version control, and using JIRA to monitor progress. By using vagrant, I set up a number of servers that would automatically communicate with a puppet master and carry out puppet runs at scheduled intervals. The generation and signing of the certificates by the master was all fully automated. 

I was tasked with creating an environment that would launch Jenkins, Jira, Nexus, Zabbix and UrbanCode-Deploy using Docker. By using the Dockerfile convention, I created containers that would deploy each tool as specified. Through the use of docker compose I was able to deploy all the containers at once. I also used docker swarm to manage the containers. 

	sudo vim atlassian-jira/WEB-INF/cl   asses/jira-application.properties

jira.home =/var/jira 

<h2><b> removing images and containers </b></h2>
<b>containers </b>
Kill containers and remove them:

	docker rm $(docker kill $(docker ps -aq))

<b>images</b>

	#removes a specific image
	docker rmi the_image     
	
However, if you need to remove multiple you could use:
Remove all images

 	docker rmi $(docker images -qf "dangling=true")
 	docker rmi $(docker images -q)

You could use grep to remove all except my-image and ubuntu

  	docker rmi $(docker images | grep -v 'ubuntu\|my-image' | awk {'print $3'})
  	
Note: Replace kill with stop for graceful shutdown




