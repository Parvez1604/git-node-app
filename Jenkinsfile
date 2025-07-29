pipeline {
  agent any

  environment {
    IMAGE = "yourdockerhubusername/node-ci-app"
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/YOUR_USERNAME/node-ci-app.git'
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
