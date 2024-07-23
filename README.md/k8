STEPS to install eks-server
--------------------------------------
step1: launch a ec2 machine (amazonlinux - recomended)
step2: create a IAM role with AdministrationAccess and attach with ec2 machine
step3:install kubectl on ec2 machine
-------------------
$ curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.25.6/2023-01-30/bin/linux/amd64/kubectl
$ chmod +x ./kubectl
$ mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
$ kubectl version --short --client
------------------
step4: install eksctl 
------------------------
$ curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
$ sudo mv /tmp/eksctl /usr/local/bin
$ eksctl version 
----------------------------
step5: create eks cluster with command 
$ eksctl create cluster --name udhu-cluster --node-type t2.large --nodes 3 --region ap-southeast-1
	-->from above command to create cluster with 3 machines in singapoor region 
-->it takes minimum 15 minuites to create cluster 
----------------------------
step6: After cluster creation to login into cluster it needs a pluggin called "aws-iam-authenticator pluggin" (when launch amazon linux it will not ask plugin setup)  
--------------
$ curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.9/aws-iam-authenticator_0.5.9_linux_amd64
$ chmod +x ./aws-iam-authenticator
$ mkdir -p $HOME/bin && cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$PATH:$HOME/bin
$ echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc
$ aws-iam-authenticator help
-------------
step7: perform ($ kubectl get node ) it will display cluster nodes 
step8: To delete cluster
----------
-->to delete EKS cluster 
$ eksctl delete cluster udhu-cluster 
$ eksctl delete cluster udhucluster --region ap-southeast-1
-->above command delete cluster and it will take few minuites to delete 
-----------
$ eksctl delete cluster thej-cluster --region ap-south-1 
======================================================================
$ eksctl create cluster --name=udhu-cluster --region=ap-southeast-1 --node-type=<node-instance-type> --nodes=<number-of-nodes>
---------------------------------------------------------------------------------------------------
$ eksctl create cluster --name=udhu-cluster --region=ap-southeast-1 --node-type=t2.large --nodes=3
--------------------------------------------------------------------
$ eksctl delete cluster --name=udhu-cluster --region=ap-southeast-1
---------------------------------------------------------------------------------------------------------------------------------  

PROMOTHEUS AND GRAFANA
-------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------
MINIKUBE
--------------------------------------------------------------------------------------------------------------------------

installation eks cluster creation after minikube process 
------------------------------------------------------------------------------------------------------------------------
______________________________________________________________________________________________________

The Architecture
In order to complete this project we will utilize Helm, Prometheus and Grafana, Minikube will be used to serve the Kubernetes Cluster.
-------------------------------------------------------------------------------------------------------------------------------------------

The process begins for Prometheus:
Fristly we will launch the Minikube Cluster.
minikube installation 
--------------------------------------------------------------------------------------------------------------------------------------------
 
$minikube start --vm-driver=<driver>   # Replace <driver> with your hypervisor driver (virtualbox, vmware, etc.)
$ minikube status
$ brew install helm
$ kubectl create namespace monitoring
$ kubectl create namespace monitoring
---------------------------------------------------------------------------------------------------------------------------------------------
Once complete we will go on to add a helm chart:
-------------------------------------------------------------------------------------------------------------------------------------------
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

$ helm repo update
--------------------------------------------------------------------------------------------------------------------------------------------

Once completed we will install the required configurations i.e. Prometheus controller, configmap etc. Essentially installing Prometheus on the cluster
--------------------------------------------------------------------------------------------------------------------------------------------------
$ helm install prometheus prometheus-community/prometheus --namespace monitoring
$ kubectl get pods -n monitoring
$ kubectl get svc -n monitoring
--------------------------------------------------------------------------------------------------------------------------------------------------
All of these are created using the cluter ip, but for this proejct we want to expose the prometheus server in order to see what the api looks like and look into queries that can be created on it. To do this we will convert the prometheus-server service from ClusterIP to NodePort service.
------------------------------------------------------------------------------------------------------------------------------------------------------------

$ kubectl expose service prometheus-server --namespace monitoring --type=NodePort --target-port=9090 --name=prometheus-server-ext\
$ minikube ip
$ http://192.168.105.2:32535
------------------------------------------------------------------------------------------------------------------------------------------------------------
Grafana installation
-------------------------------------------------------------------------------------------------------------------------------------------------------------
$ helm repo add grafana https://grafana.github.io/helm-charts
---------------------------------------------------------------------------------------------------------------------------------------------------------
Now in the same monitoring namespace we will install Grafana using helm chart
-----------------------------------------------------------------------------------------------------------------------------------------------------------
$ helm install grafana grafana/grafana --namespace monitoring
$ kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
$ kubectl expose service grafana --namespace monitoring --type=NodePort --target-port=3000 --name=grafana-ext
$ http://192.168.105.2:31173
----------------------------------------------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
