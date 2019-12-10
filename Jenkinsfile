pipeline {

  
  
  environment {
    registry = "sanyambatra/demo-pipeline"
    registryCredential = 'docker-hub'
    dockerImage = ''
    
  }

stages {

stage('Checkout') {
  agent any

steps {

checkout scm

}

}

stage('Build') {
  agent {
    docker { image 'sanyambatra/cust_img:2' }
  }

steps {

sh 'dotnet build aspnetapp.sln'

}
}
  /*stage('Build image') {
    steps {
      script{
      dockerImage=docker.build registry + ":$BUILD_NUMBER"
      }
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
  stage('Terraform') {
    steps {
      script {
        sh 'terraform init'
      }
    }
  }*/
}
}
