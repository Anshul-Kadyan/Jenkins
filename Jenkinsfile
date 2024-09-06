pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'recipient@example.com' // Set the recipient email address here
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Add build steps here
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Add test steps here
            }
            post {
                always {
                    script {
                        def testLogs = findFiles(glob: 'test-logs/*.log')
                        if (testLogs) {
                            emailext (
                                to: "${EMAIL_RECIPIENT}",
                                subject: "Unit and Integration Tests Status - ${currentBuild.currentResult}",
                                body: "The unit and integration tests have ${currentBuild.currentResult}. Please find the attached logs.",
                                attachmentsPattern: 'test-logs/*.log'
                            )
                        } else {
                            emailext (
                                to: "${EMAIL_RECIPIENT}",
                                subject: "Unit and Integration Tests Status - ${currentBuild.currentResult}",
                                body: "The unit and integration tests have ${currentBuild.currentResult}. No log files were found."
                            )
                        }
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Add code analysis steps here
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Add security scan steps here
            }
            post {
                always {
                    script {
                        def securityLogs = findFiles(glob: 'security-logs/*.log')
                        if (securityLogs) {
                            emailext (
                                to: "${EMAIL_RECIPIENT}",
                                subject: "Security Scan Status - ${currentBuild.currentResult}",
                                body: "The security scan has ${currentBuild.currentResult}. Please find the attached logs.",
                                attachmentsPattern: 'security-logs/*.log'
                            )
                        } else {
                            emailext (
                                to: "${EMAIL_RECIPIENT}",
                                subject: "Security Scan Status - ${currentBuild.currentResult}",
                                body: "The security scan has ${currentBuild.currentResult}. No log files were found."
                            )
                        }
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Add deployment steps here
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
                // Add integration tests steps here
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Add deployment steps here
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}





