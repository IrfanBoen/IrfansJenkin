pipeline {
    agent any
    
    stages {
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Capture the output of the tests to a log file
                sh '''
                    mvn test | tee unit-tests.log
                '''
            }
            post {
                always {
                    echo 'Archiving and sending email after Unit and Integration Tests...'
                    archiveArtifacts artifacts: 'unit-tests.log', allowEmptyArchive: true
                    emailext subject: "Unit and Integration Tests",
                             body: "Unit and Integration Tests stage for build ${currentBuild.fullDisplayName} is complete and: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                             to: 'IrfanBoenardi1@gmail.com',
                             attachmentsPattern: 'unit-tests.log'
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
                // Capture the output of the security scan to a log file
                sh '''
                    dependency-check.sh | tee security-scan.log
                '''
            }
            post {
                always {
                    echo 'Archiving and sending email after Security Scan...'
                    archiveArtifacts artifacts: 'security-scan.log', allowEmptyArchive: true
                    emailext subject: "Security Scan",
                             body: "Security Scan stage for build ${currentBuild.fullDisplayName} is complete and: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                             to: 'IrfanBoenardi1@gmail.com',
                             attachmentsPattern: 'security-scan.log'
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
                     to: 'IrfanBoenardi1@gmail.com'
        }
    }
}
