pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Running'
            }
        }
        stage('install node modules') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build:ssr'
            }
        }
        stage('Test') {
            steps {
                sh 'ng run test'
            }
        }        
        stage('Deploy') {
            steps {
                sh 'pm2 restart all'                
            }
        }             
    }
}