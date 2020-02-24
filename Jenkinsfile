pipeline {
  agent none
  stages {    
    stage('Fetch dependencies') {      
      steps {
        sh 'npm install'        
      }
    }
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
    }
    stage('Lint') {
      agent {
        docker 'circleci/node:9.3-stretch-browsers'
      }
      steps {
        unstash 'node_modules'
        sh 'yarn lint'
      }
    }
    stage('Unit Test') {
      agent {
        docker 'circleci/node:9.3-stretch-browsers'
      }
      steps {
        unstash 'node_modules'
        sh 'yarn test:ci'
        junit 'reports/**/*.xml'
      }
    }
    stage('E2E Test') {
      agent {
        docker 'circleci/node:9.3-stretch-browsers'
      }
      steps {
        unstash 'node_modules'
        sh 'mkdir -p reports'
        sh 'yarn e2e:pre-ci'
        sh 'yarn e2e:ci'
        sh 'yarn e2e:post-ci'
        junit 'reports/**/*.xml'
      }
    }
    stage('Compile') {
      agent {
        docker 'circleci/node:9.3-stretch-browsers'
      }
      steps {
        unstash 'node_modules'
        sh 'yarn build:prod'
        stash includes: 'dist/', name: 'dist'
      }
    }
    stage('Build and Push Docker Image') {
      agent any
      environment {
        DOCKER_PUSH = credentials('docker_push')
      }
      steps {
        unstash 'dist'
        sh 'docker build -t $DOCKER_PUSH_URL/frontend .'
        sh 'docker login -u $DOCKER_PUSH_USR -p $DOCKER_PUSH_PSW $DOCKER_PUSH_URL'
        sh 'docker push $DOCKER_PUSH_URL/frontend'
      }
    }
  }
}