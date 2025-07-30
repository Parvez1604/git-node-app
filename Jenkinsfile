pipeline {
  agent{
    docker{
      image 'node:lts'
      args '-u 0:0'
    }

  environment {
    IMAGE = "parvez1604/node-ci-app"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch:'main', url: 'https://github.com/Parvez1604/git-node-app.git'
      }
    }

    stage('Install') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE .'
      }
    }

    stage('Push to DockerHub') {
      steps {
        withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
          sh 'docker push $IMAGE'
        }
      }
    }
  }
}
