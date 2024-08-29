pipeline {
    agent any
    stages {
        stage('Copy Log File') {
            steps {
                echo 'Copying log file...'
                bat 'copy C:\\Users\\User\\Pictures\\Saved Pictures\\Log.jpg .'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
            }
            post {
                always {
                    echo 'Archiving and sending email after Unit and Integration Tests...'
                    archiveArtifacts artifacts: 'Log.jpg', allowEmptyArchive: false
                    emailext subject: "Unit and Integration Tests",
                             body: "Unit and Integration Tests stage for build ${currentBuild.fullDisplayName} is complete with result: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
                             to: 'IrfanBoenardi1@gmail.com',
                             attachmentsPattern: 'Log.jpg'
                }
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
