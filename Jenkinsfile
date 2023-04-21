pipeline {
  agent any

  stages {
    stage ('Build Image') {
      steps {
        script {
          dockerapp = docker.build("soccolint/juice-shop:${env.BUILD_ID}", '-f ./Dockerfile ./' )
        }
      }
    }
    
    stage ('Push Imagem') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            dockerapp.push('latest')
            dockerapp.push("${env.BUILD_ID}")
          }
        }
      }
    }

    stage ('Deploy Kubernets') {
      environment {
        tag_version = "${env.BUILD_ID}"
      }
      steps {
        withKubeConfig([credentialsId: 'kubeconfig']) {
          sh 'microk8s kubectl apply -f ./juice-shop.yaml'
        }
      }
    }

  }
}