pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // Polls the GitHub repository every minute
    }
    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Building the code using Maven.'
                echo 'Tool: Maven'
                // Example: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Running unit and integration tests.'
                echo 'Tool: JUnit (Java), Mocha (Node.js)'
                // Example: sh 'mvn test' or 'npm test'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/test-logs/*.log', allowEmptyArchive: true
                    emailext (
                        subject: "Unit and Integration Tests Results: Job ${env.JOB_NAME}",
                        body: "The unit and integration tests have completed. Check the attached logs for details.\n\nStatus: ${currentBuild.currentResult}\nLink: ${env.BUILD_URL}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: '**/test-logs/*.log',
                        replyTo: "work.kadyan@gmail.com",
                        compressLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Analyzing the code with SonarQube.'
                echo 'Tool: SonarQube'
                // Example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Performing a security scan with Snyk.'
                echo 'Tool: Snyk'
                // Example: sh 'snyk test'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/security-logs/*.log', allowEmptyArchive: true
                    emailext (
                        subject: "Security Scan Results: Job ${env.JOB_NAME}",
                        body: "The security scan has completed. Check the attached logs for details.\n\nStatus: ${currentBuild.currentResult}\nLink: ${env.BUILD_URL}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: '**/security-logs/*.log',
                        replyTo: "work.kadyan@gmail.com",
                        compressLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploying the application to a staging server.'
                echo 'Tool: AWS CLI'
                // Example: sh 'aws deploy ...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Running integration tests on staging environment.'
                echo 'Tool: Selenium, Postman'
                // Example: sh 'selenium test' or 'postman run ...'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying the application to a production server.'
                echo 'Tool: AWS CLI'
                // Example: sh 'aws deploy ...'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
        }
    }
}



