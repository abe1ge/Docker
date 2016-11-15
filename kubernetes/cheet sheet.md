<h1> User guide </h1>

<h2> intro to kubernetes </h2>

I also recommend the interactive exercise found on the kubernetes website http://kubernetes.io/docs/tutorials/kubernetes-basics/
This goes through all the different aspects of kubernetes and gives you a virtual vm to quickly experiment on

<h2> getting basic information </h2>

To interact with kubernetes you use the command kubectl can be pronounced kube-controle, you can see check if everything is installed by typing the following command.

	$ kubectl -version
	
to see Cluster details

	$ kubectl cluster-info
	Kubernetes master is running at http://localhost:8080                                          
	kubernetes-dashboard is running at http://localhost:8080/api/v1/proxy/namespaces/kube-system/services/kubernetes-dashboard 
	
Kubernetes can be accessed through a ui interface using the dashboard, if not already set up correctly you can go onto the following page https://github.com/kubernetes/dashboard to initialize it. 

In practice you would not deploy anything on the master machine and by default kubernetes doesn't let you. the master is there only to set up and control all the nodes and pods. if you do for any reason want to lunch pods on the master you can do so by running the following line.
	
	$ kubectl taint nodes --all dedicated-
	
What this does is make all nodes available to be utilised. I don't currently know if there is any way to undo this so tread carefully.

You can see all nodes connected to you master by running the following line.
	
	$ kubectl get nodes
	NAME           STATUS    AGE                                                               
	abel.qac.local   Ready     19m 
	
the name in most cases is the FQDN of your machine. Currently there are no nodes connected to my master. this can be done by running the kubeadm join command with the token and ipaddress given to you when you first run kubeadm init on your master.

	kubeadm join --token <token> <master-ip>
	
<h2> Deploying your first container </h2>

Deploying an container in kubernetes is much like running a container with docker.

	kubectl run <app name> --image-<image> --port=<port>
	
To start with we are going to deploy a container using the image ubuntu. 
	
	$ kubectl run ubuntu --image=ubuntu 
	deployment "ubuntu" created

Now that we have deployed a container we want to see all our deployments. This is done with get deploy

	$ kubectl get deploy
	NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE         
	ubuntu                1         1         1            1           3m   

You have to remember that by default that kubernetes does not deploy any container on the master machines therefore if you do not have any nodes the container would not be available and under the available heading it would be 0, if it is not possible for you to be to connect a node, taint the master using the commands shown above.

When you deploy an container, a pod is automatically created and that container is put into that pod. you can see all your pods by running the following command.

	$ kubectl get pods
	NAME                                  READY     STATUS             RESTARTS   AGE            
	ubuntu-3899562429-va960               1/1       Running            0          12m  

Now you may want more information on your pod then just if it is running and how long it has been running. You can do this by using the describe option. more information can be found on describe at http://kubernetes.io/docs/user-guide/kubectl/kubectl_describe/ 
Describe is a good way to debug your pod if there is anything wrong with it.
	
	$ kubectl describe pods
	Name:           ubuntu-1011661739-137g3                                                     
	Namespace:      default                                                                     
	Node:           a8ba4c41d6f8/172.17.0.80                                                    
	Start Time:     Tue, 15 Nov 2016 10:48:17 +0000                                             
	Labels:         pod-template-hash=1011661739                                                
        	        run=ubuntu                                                                  
	Status:         Running                                                                     
	IP:             172.18.0.3 
	...

For more debugging information you can also use the logs option just like you could do with docker for a container
	
	$ kubectl logs ubuntu-1011661739-137g3
	ubuntu App Started At: 2016-11-15T10:59:30.065Z | Running On:  ubuntu-1011661739-137g3 

Remembering the pods name is really hard with all the numbers and you might find it easier to create a variable that points to the name using export. if you are running only one pod you can name it using the following command to passing a name to the pod name

	$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
	
This will get the pod name and assign it to the variable POD_NAME, if you have a lot of pods running you run the following command to get all the pods name and do export pod_name= actual_podname indivdualy 

	$ kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}'
	pod1-3242342342
	pod2-2342342343
	pod3-2342153234
	
	$ export POD1_NAME=pod1-3242342342
	$ export POD2_NAME=pod2-2342342343
	$ export POD3_NAME=pod3-2342153234

Now if you want to get the logs for pod2 all you need to run is

	$ kubectl logs $POD1_NAME
	pod1  App Started At: 2016-11-15T11:58:09.015Z | Running On:  kubernetes-bootcamp-390780338-owimp
	
	#if the pod no longer exisit you can remove the vairable by running the following command
	$ unset POD1_NAME
	
	#also if for any reason you you forgot what variable you gave your pod you can find out by simply running env
	$ env
	
<h3> going into a container </h3>

To go inside a container is exactly the same as you would in docker

	kubectl exec -ti $POD_NAME bash
	
