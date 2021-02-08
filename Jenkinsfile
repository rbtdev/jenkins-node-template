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
        stage('Deploy to Staging') {
            agent none
            when {
                branch 'master'
            }
            stages {
                stage('Staging Approval') {
                    steps {
                        input "Deploy to satging?"
                    }
                }
                stage('Deploy to Staging') {
                    steps {
                        sh 'echo "Deploy to staging environment here"'
                    }
                }
            }
        }
    }
}
