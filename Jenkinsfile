pipeline {
  agent {
    kubernetes {
      defaultContainer 'kaniko'
      yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  volumes:
  - name: dockersock
    hostPath:
      path: /var/run/docker.sock
  - name: kubeconfig
    hostPath:
      path: /opt/kubernetes/storage/.kube
  containers:
  - name: k8s-helm
    image: lachlanevenson/k8s-helm:v3.6.0
    command:
    - cat
    tty: true
    volumeMounts:
      - name: kubeconfig
        mountPath: "/opt/.kube"
'''
    }
  }
  stages {
    stage('checkout') {
      checkout scm
      container('k8s-helm') {
        stage('install mongodb') {
          steps {
            sh "helm upgrade \
                --install mongodb \
                --namespace app \
                -f ./helm/mongodb/values-production.yaml \
                ./helm/mongodb"
          }
        }
//         stage('install rabbitmq') {
//           sh "helm upgrade \
//                 --install rabbitmq \
//                 --namespace app \
//                 -f ./helm/rabbitmq/values-production.yaml \
//                 ./helm/rabbitmq"
//         }
//         stage('install minio') {
//           sh "helm repo add minio https://charts.min.io"
//           sh "helm upgrade \
//                 --install minio \
//                 --namespace app \
//                 -f ./helm/minio/values-production.yaml \
//                 minio/minio"
//         }
//         stage('install es') {
//           sh "helm repo add elastic https://helm.elastic.co"
//           sh "helm upgrade \
//                 --install es \
//                 --namespace app \
//                 -f ./helm/es/values-production.yaml \
//                 elastic/elasticsearch"
//         }
      }
    }
  }
}
