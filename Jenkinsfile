pipeline {
  agent any
  environment {
    KUBECONFIG = credentials('kubeconfig') // Jenkins credential with kubeconfig
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-app-image:latest .'
      }
    }
    stage('Push') {
      steps {
        withDockerRegistry([credentialsId: 'dockerhub', url: '']) {
          sh 'docker push my-app-image:latest'
        }
      }
    }
    stage('Deploy') {
      steps {
        sh 'kubectl apply -f k8s/manifests/deployment.yaml'
        sh 'kubectl apply -f k8s/manifests/service.yaml'
      }
    }
  }
}