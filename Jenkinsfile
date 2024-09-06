pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                echo 'Using build tool: Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Using test tools: JUnit (Java), Mocha (Node.js)'
            }
            post {
                always {
                    emailext (
                        subject: "Unit and Integration Tests Results",
                        body: "The unit and integration tests have completed. Check the attached logs for details.\n\n${BUILD_LOG, maxLines=100, escapeHtml=true}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: '**/test-logs/*.log',
                        replyTo: "work.kadyan@gmail.com",
                        compressLog: true // Updated parameter
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                echo 'Using code analysis tool: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                echo 'Using security scan tool: Snyk'
            }
            post {
                always {
                    emailext (
                        subject: "Security Scan Results",
                        body: "The security scan has completed. Check the attached logs for details.\n\n${BUILD_LOG, maxLines=100, escapeHtml=true}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: '**/security-logs/*.log',
                        replyTo: "work.kadyan@gmail.com",
                        compressLog: true // Updated parameter
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                echo 'Using deployment tool: AWS CLI'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
                echo 'Using test tools: Selenium, Postman'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                echo 'Using deployment tool: AWS CLI'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
        always {
            echo 'Cleaning up...'
        }
    }
}





