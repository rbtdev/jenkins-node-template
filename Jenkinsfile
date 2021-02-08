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
        stage('Reading for Staging') {
            agent none
            when {
                branch 'master'
            }
            stages {
                stage('Staging Approval') {
                    steps {
                        input "Deploy to Staging?"
                    }
                }
                stage('Deploy to Staging') {
                    steps {
                        sh 'echo "Deploy to Staging environment here"'
                    }
                }
            }
        }
        stage('Ready for Production') {
            agent none
            when {
                branch 'master'
            }
            stages {
                stage('Production Approval') {
                    steps {
                        input "Deploy to Production?"
                    }
                }
                stage('Deploy to Production') {
                    steps {
                        sh 'echo "Deploy to Production environment here"'
                    }
                }
            }
        }
    }
}
