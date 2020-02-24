pipeline {
agent any
 
  tools {
    nodejs 'nodejs'
  }
 
  stages {
    stage('Build') {
      steps {
        echo '$nodejs'
        //sh 'npm install'
      }
    }
  }
}


    /*
    stage('Code Quality') {
      steps {
        container('Sonarqube Scanner') {
          withSonarQubeEnv('Sonarqube') {
            sh '/usr/local/sonar-scanner'
          }
          timeout(time: 10, unit:'MINUTES') {
            waitForQualityGate abortPipeline: true
          }
        }
      }
    }*/
    