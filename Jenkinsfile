pipeline {

agent any
  tool name: 'terraform_tool', type: 'org.jenkinsci.plugins.terraform.TerraformInstallation'
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
        /*withCredentials([azureServicePrincipal('azure-cred')]) {
    sh 'terraform apply -auto-approve'
}*/
      }
    }
  }
}
}
