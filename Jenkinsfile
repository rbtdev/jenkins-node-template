pipeline {
    agent { docker { image 'node:14-alpine' } }
    stages {
        stage('Build') {
            steps {
                sh 'npm --version'
                sh 'node --version'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy Approval') {
            agent none
            steps {
                input "Deploy to prod?"
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo "Deploy to cloud here"'
            }
        }
    }
}
