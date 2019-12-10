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
      dockerImage=docker.build("dotnetapp_img:${env.BUILD_ID}")
      }
    }
  }
  stage('Push image') {
    steps {
      script {
        withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'password_var', usernameVariable: 'username_var')]) {
      docker.withRegistry( '', registryCredential ) {
          sh 'docker login -u ${username_var} -p ${password_var}'
        dockerImage.push()
      }  
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
