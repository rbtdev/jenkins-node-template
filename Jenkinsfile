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
        stage('Staging Approval') {
            agent none
            steps {
                input "Deploy to satging?"
            }
        }
        stage('Deploy to Staging') {
            steps {
                sh 'echo "Deploy to staging environment here"'
            }
        }
        stage('Production Approval') {
            agent none
            steps {
                input "Deploy to Production?"
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'echo "Deploy to production environment here"'
            }
        }
    }
}
