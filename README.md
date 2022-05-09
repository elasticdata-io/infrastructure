# infrastructure

## Install k8s dashboard 

```
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
helm install dashboard kubernetes-dashboard/kubernetes-dashboard
kubectl --namespace default port-forward svc/dashboard-kubernetes-dashboard 8443:443
```

## Install Jenkins

```
cd ./helm/jenkins
helm repo add jenkins https://charts.jenkins.io
helm install jenkins --namespace default -f values-production.yaml jenkins/jenkins
```

## Install Mongodb

```
cd ./helm
helm upgrade --install mongodb --namespace app -f ./mongodb/values-production.yaml ./mongodb
```

## Install Docker registry 

```
cd ./helm/docker-registry
helm repo add twuni https://helm.twun.io
helm install docker-registry --namespace default -f values-production.yaml twuni/docker-registry
```
