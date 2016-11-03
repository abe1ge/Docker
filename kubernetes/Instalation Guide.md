

# Installing Kubernetes

this installtion guide is following the offical instalation guide found on the kubernetes website. I have detailed my personl experince and what i thought was relevent but if you perfer a more detailed tutorial go to http://kubernetes.io/docs/getting-started-guides/kubeadm/   
<h3> Requirements </h3>

The official website recomands that you install kubernetes on <b>16.04, CentOS 7 or HypriotOS v1.0.1</b>. it is possiable to install on later versions of ubuntu and other OSs but further work may be required. The website also recommand that the machine kubernetes is being installed on has a minimum of 1GB ram, 

<h4> upgrading to ubuntu 16.04 from 14.04</h4>
If you are running ubuntu 14.04 and want to upgrade to the latest version, you can do so by running the following two lines.

	$ sudo apt-get install update-manager-core
	$ sudo do-release-upgrade
<h2> Step 01: Installing on ubuntu 16.04</h2>
you have to be a root user to run the following lines, you can do so by runnig 'sudu su -'

	$ sudu su -
	$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
	$ echo deb http://apt.kubernetes.io/ kubernetes-xenial main  >> /etc/apt/sources.list.d/kubernetes.list
	$ apt-get update
	$ Install docker if you don't have it already.
	$ apt-get install -y docker.io
	$ apt-get install -y kubelet kubeadm kubectl kubernetes-cni


Now to initialise you master you run kubeadm init:
	
	$ kubeadm init
the output will look something like this

	<master/tokens> generated token: "9aa8bd.31a3aa77563aa931"
	<master/pki> created keys and certificates in "/etc/kubernetes/pki"
	<util/kubeconfig> created "/etc/kubernetes/admin.conf"
	<util/kubeconfig> created "/etc/kubernetes/kubelet.conf"
	<master/apiclient> created API client configuration
	<master/apiclient> created API client, waiting for the control plane to become ready
	<master/apiclient> all control plane components are healthy after 24.910032 seconds
	<master/apiclient> waiting for at least one node to register and become ready
	<master/apiclient> first node is ready after 6.002629 seconds
	<master/discovery> created essential addon: kube-discovery, waiting for it to become ready
	<master/discovery> kube-discovery is ready after 10.502503 seconds
	<master/addons> created essential addon: kube-proxy
	<master/addons> created essential addon: kube-dns

	Kubernetes master initialised successfully!

	You can now join any number of machines by running the following on each node:

	kubeadm join --token 9aa8bd.31a3aa77563aa931 172.31.1.61
	
Make a record of the kubeadm join command that kubeadm init outputs. You will need this in a moment. The key included here is secret, keep it safe — anyone with this key can add authenticated nodes to your cluster.

<h2> Step 02: Installing a pod network </h2>
It is necessary to do this before you try to deploy any applications to your cluster, and before kube-dns will start up. Note also that kubeadm only supports CNI based networks and therefore kubenet based networks will not work.

There are currently four project you can use to set up your pod network, for this project we will be using <a href="https://github.com/weaveworks/weave-kube">Weave Net</a> but other projects can be found <a href="http://kubernetes.io/docs/admin/addons/" target="_blank">here</a> 
to install Weave Net pod network run the following command

	kubectl create -f https://git.io/weave-kube
	
	



