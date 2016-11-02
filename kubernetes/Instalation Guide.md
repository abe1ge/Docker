<h1> Installing Kubernetes </h1>

this installtion is taken from http://kubernetes.io/docs/getting-started-guides/kubeadm/  
<h3> Requirements </h3>

The official website recomands that you install kubernetes on <b>16.04, CentOS 7 or HypriotOS v1.0.1</b>. it is possiable to install on later versions of ubuntu and other OSs but further work may be required. The website also recommand that the machine kubernetes is being installed on has a minimum of 1GB ram, 
<h2> Installing on ubuntu 16.04</h2>

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo deb http://apt.kubernetes.io/ kubernetes-xenial main  >> /etc/apt/sources.list.d/kubernetes.list
# apt-get update
# # Install docker if you don't have it already.
# apt-get install -y docker.io
# apt-get install -y kubelet kubeadm kubectl kubernetes-cni
