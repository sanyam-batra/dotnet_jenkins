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

/*stage('Build') {

steps {

sh 'dotnet build aspnetapp.sln'

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
  }*/
  stage('Terraform') {
    steps {
      script {
        sh 'terraform init'
    withCredentials([azureServicePrincipal('azure-cred')]) {
    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
}
      }
    }
  }
}
}
