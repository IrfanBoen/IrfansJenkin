pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh 'mvn clean install'  
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                sh 'sonar-scanner' 
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'dependency-check --project pipeline --scan .'  
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                sh 'scp -i my-key.pem target/*.jar ec2-user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'curl -X GET http://staging-server/api/health'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh 'scp -i my-key.pem target/*.jar ec2-user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            mail to: 'IrfanBoenardi1@gmail.com',
                 subject: "SUCCESS: Pipeline ${currentBuild.fullDisplayName}",
                 body: "Pipeline succeeded: ${currentBuild.fullDisplayName}"
        }
        failure {
            mail to: 'developer@example.com',
                 subject: "FAILURE: Pipeline ${currentBuild.fullDisplayName}",
                 body: "Pipeline failed: ${currentBuild.fullDisplayName}",
                 attachmentsPattern: '**/target/**/*.log'
        }
    }
}

