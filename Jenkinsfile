pipeline {

agent any
  environment {
    registry = "sanyambatra/demo-pipeline"
    registryCredential = 'docker-hub'
    dockerImage = ''
  }

stages {

stage('Checkout') {

steps {

checkout scm

}

}

stage('Build') {

steps {

sh 'dotnet build aspnetapp.sln'

}
}
  stage('Build image') {
    steps {
      dockerImage=docker.build registry + ":$BUILD_NUMBER"
    }
  }
  stage('Push image') {
    steps {
      script {
        docker.withRegistry( '', registryCredential ) {
        dockerImage.push()
      }   
      }
    }
  }
}
}
