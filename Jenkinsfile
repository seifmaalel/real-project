pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t seifeddinemaalel/real-project-front ui/'
        sh 'docker build -t seifeddinemaalel/real-project-back api/'
        sh 'docker build -t seifeddinemaalel/real-project-data .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push seifeddinemaalel/real-project-front'
        sh 'docker push seifeddinemaalel/real-project-back'
        sh 'docker push seifeddinemaalel/real-project-data'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
