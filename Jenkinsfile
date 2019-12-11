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
  stage('Deploy') {
    steps {
      script {
            def customImage = docker.build("my-image:${env.BUILD_ID}","./aspnetapp/")

    customImage.inside {
                withCredentials([azureServicePrincipal('azure_cred')]) {
          sh 'az login'
                  sh 'az group create --name sanyamdemogroup --location eastus'
                  //sh 'az acr create --name sanyamregistry --resource-group sanyamdemogroup --sku Basic --admin-enabled true'
                  sh 'docker login '
                  sh 'az appservice plan create -n demoplan -g sanyamdemo --sku S1 --is-linux'
                  sh 'az webapp create -g sanyamdemo -p demoplan -n sanyamdockerdemo --runtime "DOTNETCORE|3.0"'
               
        }
    }

      }
    }
  }
}
}
