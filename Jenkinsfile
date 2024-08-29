pipeline {
    agent any
    
    stages {
        stage('Copy Log File') {
            steps {
                echo 'Copying log file...'
                bat 'copy C:\Users\User\IrfansJenkin\Log.jpg .' 
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                // Example of MVN
                // sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Example of running unit and integration tests
                // sh 'mvn test'
            }
            post {
                always {
                    echo 'Archiving and sending email after Unit and Integration Tests...'
                    archiveArtifacts artifacts: 'Log.jpg', allowEmptyArchive: true
                    emailext subject: "Unit and Integration Tests",
                             body: "Unit and Integration Tests stage for build ${currentBuild.fullDisplayName} is complete with result: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                             to: 'IrfanBoenardi1@gmail.com',
                             attachmentsPattern: 'Log.jpg'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                // Example of SonarQube
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Example of Dependency Check
                // sh 'dependency-check.sh'
            }
            post {
                always {
                    echo 'Archiving and sending email after Security Scan...'
                    archiveArtifacts artifacts: 'Log.jpg', allowEmptyArchive: true
                    emailext subject: "Security Scan",
                             body: "Security Scan stage for build ${currentBuild.fullDisplayName} is complete with result: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                             to: 'IrfanBoenardi1@gmail.com',
                             attachmentsPattern: 'Log.jpg'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example of deploying to staging
                // sh 'deploy.sh staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example of running tests on staging
                // sh 'mvn verify -Pstaging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Example of deploying to production
                // sh 'deploy.sh production'
            }
        }
    }
    
    post {
        always {
            echo 'Sending final notification email...'
            emailext subject: "Jenkins Pipeline - Final Status",
                     body: "The build ${currentBuild.fullDisplayName} has completed with status: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                     to: 'IrfanBoenardi1@gmail.com',
                     attachmentsPattern: 'Log.jpg'
        }
    }
}
