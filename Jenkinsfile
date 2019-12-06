pipeline {

agent any

stages {

stage('Checkout') {

steps {

checkout scm

}

}

stage('Build') {

steps {

bat 'dotnet build aspnetapp.sln –configuration Release'

}
}
}
}
