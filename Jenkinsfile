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
                    script {
                        // Create a report file
                        sh 'echo "Unit and Integration Tests Status: ${currentBuild.currentResult}" > unit_integration_tests_report.txt'
                        sh 'echo "Job Name: ${env.JOB_NAME}" >> unit_integration_tests_report.txt'
                        sh 'echo "Build Number: ${env.BUILD_NUMBER}" >> unit_integration_tests_report.txt'
                        sh 'echo "Build URL: ${env.BUILD_URL}" >> unit_integration_tests_report.txt'
                    }
                    archiveArtifacts artifacts: 'unit_integration_tests_report.txt', onlyIfSuccessful: true
                    emailext (
                        subject: "Unit and Integration Tests Report: ${currentBuild.currentResult} - Job ${env.JOB_NAME}",
                        body: "Unit and Integration Tests ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n\nBuild URL: ${env.BUILD_URL}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: 'unit_integration_tests_report.txt',
                        replyTo: "work.kadyan@gmail.com"
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
                    script {
                        // Create a report file
                        sh 'echo "Security Scan Status: ${currentBuild.currentResult}" > security_scan_report.txt'
                        sh 'echo "Job Name: ${env.JOB_NAME}" >> security_scan_report.txt'
                        sh 'echo "Build Number: ${env.BUILD_NUMBER}" >> security_scan_report.txt'
                        sh 'echo "Build URL: ${env.BUILD_URL}" >> security_scan_report.txt'
                    }
                    archiveArtifacts artifacts: 'security_scan_report.txt', onlyIfSuccessful: true
                    emailext (
                        subject: "Security Scan Report: ${currentBuild.currentResult} - Job ${env.JOB_NAME}",
                        body: "Security Scan ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n\nBuild URL: ${env.BUILD_URL}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: 'security_scan_report.txt',
                        replyTo: "work.kadyan@gmail.com"
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




