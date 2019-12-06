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

sh 'dotnet build aspnetapp.sln –configuration Release'

}
}
}
}
