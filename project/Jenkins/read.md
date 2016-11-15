#How to use 

to build this docker file while in this directory

	docker build -t jenkins .
	
to run it in deamnised form

	docker run --name jenkinsci -p 8080:8080 -p 50000:50000 jenkins:2.0
	
	
additional information can be found on http://blog.alexellis.io/jenkins-2-0-first-impressions/
