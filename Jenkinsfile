pipeline {
    agent any
    stages {
        stage('Build Staging') {
            steps {
                bat 'mvn clean package'
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
    }
}
