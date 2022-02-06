# ELasticsearch-Cluster-on-EKS
***Kubernetes cluster is already setuped by run team 

create Name space 
---------------------
#Kubectl create namespace elasticnamespace

Install Package manager " Helm"
-------------------------------
#wget https://get.helm.sh/helm-v3.4.1-linux-amd64.tar.gz
unpack the Helm file using the
#tar xvf helm-v3.4.1-linux-amd64.tar.gz
Move the linux-amd64/helm file to the /usr/local/bin directory
#sudo mv linux-amd64/helm /usr/local/bin

Add the Bitnami Repository and Deploy the Elasticsearch Chart
---------------------------------------------------------------
#helm repo add bitnami https://charts.bitnami.com/bitnami

Install Charts
---------------
#helm install elasticsearch --set master.replicas=3,coordinating.service.type=LoadBalancer bitnami/elasticsearch

Monitoring 
-----------
#kubectl get pods
until getting ready 1/1

Test the Connection
--------------------
#kubectl port-forward svc/elasticsearch-master 9200
#curl localhost:9200 ( from another terminal )

Check pods info :
---------------
#kubectl get pods -o wide

Check cluster services
----------------------
#kubectl get svc

Additional way :
--------------
We can deploy each role of elasticsearch pods separetly by role :

helm install elasticsearch-multi-master elastic/elasticsearch -f ./master.yaml
helm install elasticsearch-multi-data elastic/elasticsearch -f ./data.yaml
helm install elasticsearch-multi-client elastic/elasticsearch -f ./client.yaml

files are attached in github




