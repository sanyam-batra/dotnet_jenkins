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
  steps {
    script {
    def customImage = docker.build("my-image:${env.BUILD_ID}")

    customImage.inside {
        sh 'dotnet build aspnet.sln'
    }
}
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
