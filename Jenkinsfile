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
    stage ('push image'){
      steps {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
        dockerapp.push("latest")
        dockerapp.push("${env.BUILD_ID}")
      }
    }
    stage ('deploy kubernetes') {
      environment {
        tag_version = "${env.BUIL_ID}"
      }
      steps {
        withKubeConfig([credentialsId:'kubeconfigF']){
          sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/deployment.yaml'
          sh 'kubectl apply -f ./k8s/deployment.yaml'
          
        }
      }
    }
  }
}
