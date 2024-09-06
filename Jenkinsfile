pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // Polls the GitHub repository every minute
    }
    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Building the code using Maven.'
                // Replace with actual build command
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Running unit and integration tests.'
                // Replace with actual test commands
                sh 'mvn test'
                // Create and save the test results to a file
                sh 'echo "Unit and Integration Tests Results" > unit_integration_tests_report.txt'
            }
            post {
                always {
                    script {
                        archiveArtifacts artifacts: 'unit_integration_tests_report.txt', onlyIfSuccessful: true
                    }
                    emailext(
                        subject: "Unit and Integration Tests Report: ${currentBuild.currentResult} - Job ${env.JOB_NAME}",
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n\nLink: ${env.BUILD_URL}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: 'unit_integration_tests_report.txt',
                        replyTo: "work.kadyan@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Analyzing the code with SonarQube.'
                // Replace with actual code analysis command
                sh 'sonar-scanner'
                // Create and save the code analysis results to a file
                sh 'echo "Code Analysis Results" > code_analysis_report.txt'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Performing a security scan with Snyk.'
                // Replace with actual security scan command
                sh 'snyk test'
                // Create and save the security scan results to a file
                sh 'echo "Security Scan Results" > security_scan_report.txt'
            }
            post {
                always {
                    script {
                        archiveArtifacts artifacts: 'security_scan_report.txt', onlyIfSuccessful: true
                    }
                    emailext(
                        subject: "Security Scan Report: ${currentBuild.currentResult} - Job ${env.JOB_NAME}",
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n\nLink: ${env.BUILD_URL}",
                        to: "work.kadyan@gmail.com",
                        attachmentsPattern: 'security_scan_report.txt',
                        replyTo: "work.kadyan@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploying the application to a staging server.'
                // Replace with actual deployment command
                sh 'aws deploy ...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Running integration tests on staging environment.'
                // Replace with actual test commands
                sh 'postman run ...'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying the application to a production server.'
                // Replace with actual deployment command
                sh 'aws deploy ...'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
        }
    }
}




