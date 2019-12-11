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
                  withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'passvar', usernameVariable: 'uservar')]) {
    sh 'docker login '
}
                  
                  sh 'az appservice plan create -n sanyamdemoplan -g sanyamdemogroup --sku S1 --is-linux'
                  sh 'az webapp create -g sanyamdemogroup -p sanyamdemoplan -n sanyamdemoapp --deployment-container-image-name sanyambatra/demo-pipeline:29'
                  sh 'az webapp config appsettings set --resource-group sanyamdemogroup --name sanyamdemoapp --settings WEBSITES_PORT=8000'
               
        }
    }

      }
    }
  }
}
}
