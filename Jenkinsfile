pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                sh 'dependency-check.sh'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'deploy.sh staging'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'mvn verify -Pstaging'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'deploy.sh production'
            }
        }
    }
    post {
        always {
            echo 'Sending notification emails...'
            mail to: 'IrfanBoenardi1@gmail.com',
                 subject: "Jenkins Pipeline ${currentBuild.fullDisplayName}",
                 body: "The build ${currentBuild.fullDisplayName} has finished with status: ${currentBuild.result}. Check console output at ${env.BUILD_URL} to view the results."
        }
    }
}
