<h1> User guid </h1>

<h2> intro to kubernetes </h2>

I also recommend the interactive exersise found on the kubernetes website http://kubernetes.io/docs/tutorials/kubernetes-basics/
this goes through all the different aspects of kubernetes and gives you a virtual vm to quickly experment on

<h2> getting basic information </h2>

To interact with kubernet you use the command kubectl can be pronouced kube-controle, you can see check if everything is installed by typeing the following command.

	$ kubectl -version
	
to see Cluster details

	$ kubectl cluster-info
	Kubernetes master is running at http://localhost:8080                                          
	kubernetes-dashboard is running at http://localhost:8080/api/v1/proxy/namespaces/kube-system/services/kubernetes-dashboard 
	
Kuberneties can be accessed through a ui interface using the dashboard, if not already set up correctly you can go onto the following page https://github.com/kubernetes/dashboard to initialize it. 

In practice you would not deploy anything on the master machine and by defult kubernetes doesn't let you. the master is there only to set up and controle all the nodes and pods. if you do for any reason want to lunch pods on the master you can do so by running the following line.
	
	$ kubectl taint nodes --all dedicated-
	
What this does is make all nodes availaible to be utalised. I don't currently know if there is anyway to undo this so tread carefully.

You can see all nodes connected to you master by running the following line.
	
	$ kubectl get nodes
	NAME           STATUS    AGE                                                               
	abel.qac.local   Ready     19m 
	
the name in most cases is the FQDN of your machine. currently there is no nodes connected to my master. this can be done by running the kubeadm join command with the token and ipaddress given to you when you first run kubeadm init on your master.

	kubeadm join --token <token> <master-ip>
	
<h2> Deploying your first app </h2>

running an app in kuberneties is much like running a container with docker it self.

	kubectl run <app name> --image-<image> --port=<port>
	
to start with we are going to deploy an app using the image ubuntu. 
	kubectl run ubuntu --image=ubuntu 
	
