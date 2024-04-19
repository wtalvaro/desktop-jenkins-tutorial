pipeline {
  agent any
  stages {
    stage ('build image') {
      steps {
        script {
          dockerapp = docker.build('wtalvaro/desktop-jenkins-tutorial', '-f ./src/Dockerfile ./src')
        }
      }
    }
  }
}
