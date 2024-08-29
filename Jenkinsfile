pipeline {
    agent any
    stages {
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
                // sh 'mvn test'
            }
            post {
                always {
                    echo 'Sending email after Unit and Integration Tests...'
                    mail to: 'IrfanBoenardi123@gmail.com',
                         subject: "Unit and Integration Tests",
                         body: "Unit and Integration Tests stage for build ${currentBuild.fullDisplayName} is complete and: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
			 attachLog: true
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
		// Example of sonarqube
                // sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
		// example of dependency check
                // sh 'dependency-check.sh'
            }
            post {
                always {
                    echo 'Sending email after Security Scan...'
                    mail to: 'IrfanBoenardi123@gmail.com',
                         subject: "Security Scan",
                         body: "Security Scan stage for build ${currentBuild.fullDisplayName} is completed and: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}.",
			 attachLog: true
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
		// example of deploying to staging
                // sh 'deploy.sh staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
		// example of running tests on staging
                // sh 'mvn verify -Pstaging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
		// example of deploying to production
                // sh 'deploy.sh production'
            }
        }
    }
    post {
        always {
            echo 'Sending final notification email...'
            mail to: 'IrfanBoenardi123@gmail.com',
                 subject: "Jenkins Pipeline - Final Status",
                 body: "The build ${currentBuild.fullDisplayName} has completed with status: ${currentBuild.result}. Check the console output at ${env.BUILD_URL}."
        }
    }
}
