pipeline {
  agent any

  stages {
    stage ('Build Image') {
      steps {
        script {
          dockerapp = docker.build("soccolInt/juice-shop", '-f ./Dockerfile ./' )
        }
      }
    }
  }
}
