pipeline {
    agent any
    stages {
        stage('Build Staging') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war*'
                }
            }
        }
        stage('Deploy to staging') {
            steps {
                build job: 'Deploy-to-staging'
            }
            post {
                success {
                    echo 'Code deployed to staging'
                }
                failure {
                    echo 'Deploymnet to staging failed'
                }
            }
        }
        stage('Build Production') {
            steps {
                sh 'mvn -Pprod clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war*'
                }
            }
        }
        stage('Deploy to production') {
            steps {
                timeout(time:5, unit:'DAYS') {
                    input message:'Approve PRODUCTION Deployment?'
                }
                build job: 'Deploy-to-production'
            }
            post {
                success {
                    echo 'Code deployed to production'
                }
                failure {
                    echo 'Deploymnet to production failed'
                }
            }
        }
    }
}
