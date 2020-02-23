pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo 'Checkout master branch'
        checkout scm
        dir('webapp') {
          sh 'npm install'
        }
      }
    }
    stage('Build') {
      steps {
        echo 'Building..'
        dir('webapp') {
          sh 'npm run ng -- build --prod --baseHref=/webapp/ -optimization=true'
        }
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying....'
      }
    }
  }
  post {
    success {
      slackSend(color: '#00FF00', message: "Build Successful")
    }
    failure {
      slackSend(color: '#FF0000', message: "Build Failed")
    }
  }
}