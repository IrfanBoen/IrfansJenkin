pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // sh 'mvn test'
            }
            post {
                always {
                    echo 'Sending email after Unit and Integration Tests...'
                    mail to: 'IrfanBoenardi1@gmail.com',
                         subject: "Jenkins Pipeline - Unit and Integration Tests",
                         body: "The Unit and Integration Tests stage for build ${currentBuild.fullDisplayName} has completed with status: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}."
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // sh 'dependency-check.sh'
            }
            post {
                always {
                    echo 'Sending email after Security Scan...'
                    mail to: 'IrfanBoenardi1@gmail.com',
                         subject: "Jenkins Pipeline - Security Scan",
                         body: "The Security Scan stage for build ${currentBuild.fullDisplayName} has completed with status: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}."
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // sh 'deploy.sh staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // sh 'mvn verify -Pstaging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // sh 'deploy.sh production'
            }
        }
    }
    post {
        always {
            echo 'Sending final notification email...'
            mail to: 'IrfanBoenardi1@gmail.com',
                 subject: "Jenkins Pipeline - Final Status",
                 body: "The build ${currentBuild.fullDisplayName} has completed with status: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}."
        }
    }
}
