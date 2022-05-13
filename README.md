# infrastructure

## Install k8s dashboard 

```
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
helm install dashboard kubernetes-dashboard/kubernetes-dashboard
kubectl --namespace default port-forward svc/dashboard-kubernetes-dashboard 8443:443
```

## Install Cert-Manager

Add  issuer:

```
kubectl apply -f ./kubetcl/issuer.yaml
```

## Install Jenkins

```
cd ./helm
helm repo add jenkins https://charts.jenkins.io
helm upgrade --install jenkins --namespace default -f ./jenkins/values-production.yaml jenkins/jenkins
kubectl create clusterrolebinding permissive-binding --clusterrole=cluster-admin --user=admin --user=kubelet --group=system:serviceaccounts
kubectl create ns app
```

Add global variables:

* DOCKER_CONTAINER_PREFIX
* DOCKER_CONTAINER_LOGIN
* DOCKER_CONTAINER_PASSWORD

TODO: move general project to elasticdata-io
TODO: configure default build steps with jenkins env 

## Install Mongodb

```
cd ./helm
helm upgrade --install mongodb --namespace app -f ./mongodb/values-production.yaml ./mongodb
```

## Install Rabbitmq

```
cd ./helm
helm upgrade --install rabbitmq --namespace app -f ./rabbitmq/values-production.yaml ./rabbitmq
```

## Install Minio

```
cd ./helm
helm repo add minio https://charts.min.io/
helm upgrade --install minio --namespace app -f ./minio/values-production.yaml minio/minio
```

## Install Elasticsearch

```
cd ./helm
helm repo add elastic https://helm.elastic.co
helm upgrade --install es --namespace app -f ./es/values-production.yaml elastic/elasticsearch
```

## Install Docker registry 

```
cd ./helm/docker-registry
helm repo add twuni https://helm.twun.io
helm install docker-registry --namespace default -f values-production.yaml twuni/docker-registry
```
