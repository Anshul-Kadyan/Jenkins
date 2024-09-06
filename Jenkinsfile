pipeline {
    agent any
    
    environment {
        EMAIL_RECIPIENT = 'work.kadyan@gmail.com'
    }
    
    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the application...'
                echo 'Using build tool: Maven'
                // For example, 'mvn clean install' could be used here if applicable
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Using test tools: JUnit (Java), Mocha (Node.js)'
                // Example command to run tests and generate logs
                // sh 'mvn test > test-logs/test.log'
                // sh 'npm test > test-logs/test.log'
            }
            post {
                always {
                    script {
                        def logFiles = sh(script: 'ls -1 test-logs/*.log', returnStdout: true).trim()
                        if (logFiles) {
                            emailext (
                                subject: "Unit and Integration Tests Results",
                                body: "The unit and integration tests have completed. Check the attached logs for details.",
                                to: EMAIL_RECIPIENT,
                                attachmentsPattern: 'test-logs/*.log',
                                replyTo: EMAIL_RECIPIENT,
                                compressLog: true
                            )
                        } else {
                            echo 'No test log files found for attachment.'
                        }
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                echo 'Using code analysis tool: SonarQube'
                // Example command for code analysis
                // sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                echo 'Using security scan tool: Snyk'
                // Example command for security scan
                // sh 'snyk test'
            }
            post {
                always {
                    script {
                        def logFiles = sh(script: 'ls -1 security-logs/*.log', returnStdout: true).trim()
                        if (logFiles) {
                            emailext (
                                subject: "Security Scan Results",
                                body: "The security scan has completed. Check the attached logs for details.",
                                to: EMAIL_RECIPIENT,
                                attachmentsPattern: 'security-logs/*.log',
                                replyTo: EMAIL_RECIPIENT,
                                compressLog: true
                            )
                        } else {
                            echo 'No security scan log files found for attachment.'
                        }
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                echo 'Using deployment tool: AWS CLI'
                // Example command for deployment
                // sh 'aws deploy ...'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
                echo 'Using test tools: Selenium, Postman'
                // Example command for integration tests
                // sh 'run-integration-tests.sh'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                echo 'Using deployment tool: AWS CLI'
                // Example command for deployment
                // sh 'aws deploy ...'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}



