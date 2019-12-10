pipeline {
  agent any
  environment {
    registry = "sanyambatra/demo-pipeline"
    registryCredential = 'docker-hub'
    dockerImage = ''
    HOME = '/tmp'
    
  }

stages {
    
stage('Checkout') {
    
steps {
      script {
    def customImage = docker.build("my-image:${env.BUILD_ID}","./aspnetapp/")

    customImage.inside {
        checkout scm
    }
}
    

    
}
    
}

stage('Build') {
  steps {
    script {
    def customImage = docker.build("my-image:${env.BUILD_ID}","./aspnetapp/")

    customImage.inside {
        sh 'dotnet build aspnetapp.sln'
    }
}
}
}
  stage('Build image') {
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
  /*stage('Terraform') {
    steps {
      script {
        sh 'terraform init'
      }
    }
  }*/
}
}
