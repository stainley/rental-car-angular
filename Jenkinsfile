pipeline {
agent any
 
  tools {nodejs "nodejs"}
 
  stages {
    stage('Example') {
      steps {
        sh 'npm config ls'
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
    