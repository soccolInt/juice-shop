pipeline {
  agent any

  stages {
    stage ('Build Image') {
      steps {
        script {
          dockerapp = docker.build("soccolint/juice-shop", '-f ./Dockerfile ./' )
        }
      }
    }
  }
}
