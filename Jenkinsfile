pipeline {
  agent any
  stages {
    stage ('build image') {
      steps {
        script {
          dockerapp = docker.build('wtalvaro/desktop-jenkins-tutorial:${env.BUILD_ID}', '-f ./src/Dockerfile ./src')
        }
      }
    }
  }
}
