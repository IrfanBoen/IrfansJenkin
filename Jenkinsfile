pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Example of MVN
                // sh 'mvn clean package' (Ensure mvn is correctly installed and in the system PATH)
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Capture the logs if needed
                bat 'echo "Simulated Unit and Integration Tests logs" > unit_integration_tests.log'  // Using bat for Windows
            }
            post {
                always {
                    echo 'Sending email after Unit and Integration Tests...'
                    archiveArtifacts artifacts: 'unit_integration_tests.log', allowEmptyArchive: true
                    emailext subject: "Unit and Integration Tests - ${currentBuild.fullDisplayName}",
                             body: "Unit and Integration Tests stage for build ${currentBuild.fullDisplayName} is complete and: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                             to: 'IrfanBoenardi1@gmail.com',
                             attachmentsPattern: 'unit_integration_tests.log'
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Capture the logs if needed
                bat 'echo "Simulated Security Scan logs" > security_scan.log'  // Using bat for Windows
            }
            post {
                always {
                    echo 'Sending email after Security Scan...'
                    archiveArtifacts artifacts: 'security_scan.log', allowEmptyArchive: true
                    emailext subject: "Security Scan - ${currentBuild.fullDisplayName}",
                             body: "Security Scan stage for build ${currentBuild.fullDisplayName} is complete and: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                             to: 'IrfanBoenardi1@gmail.com',
                             attachmentsPattern: 'security_scan.log'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Example of deploying to staging
                // bat 'deploy.bat staging' (use bat for Windows batch scripts)
            }
        }
    }
    post {
        always {
            echo 'Sending final notification email...'
            emailext subject: "Jenkins Pipeline - Final Status",
                     body: "The build ${currentBuild.fullDisplayName} has completed with status: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                     attachLog: true,
                     to: 'IrfanBoenardi1@gmail.com'
        }
    }
}
