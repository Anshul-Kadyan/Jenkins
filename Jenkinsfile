pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // Polls the GitHub repository every minute
    }
    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build - Building the code using Maven.'
                // Echo a placeholder message to a file
                sh 'echo "Build stage completed successfully." > build_report.txt'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Running unit and integration tests.'
                // Echo test results to a file
                sh 'echo "Unit and Integration Tests Results: Tests completed successfully." > unit_integration_tests_report.txt'
            }
            post {
                always {
                    script {
                        archiveArtifacts artifacts: 'unit_integration_tests_report.txt', onlyIfSuccessful: true
                    }
                    emailext(
                        subject: "Unit and Integration Tests Report: ${currentBuild.currentResult} - Job ${env.JOB_NAME}",
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n\nUnit and Integration Tests results attached.",
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
                // Echo code analysis results to a file
                sh 'echo "Code Analysis Results: Code analysis completed successfully." > code_analysis_report.txt'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Performing a security scan with Snyk.'
                // Echo security scan results to a file
                sh 'echo "Security Scan Results: Security scan completed successfully." > security_scan_report.txt'
            }
            post {
                always {
                    script {
                        archiveArtifacts artifacts: 'security_scan_report.txt', onlyIfSuccessful: true
                    }
                    emailext(
                        subject: "Security Scan Report: ${currentBuild.currentResult} - Job ${env.JOB_NAME}",
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n\nSecurity Scan results attached.",
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
                // Echo deployment status to a file
                sh 'echo "Deployment to Staging completed successfully." > deploy_staging_report.txt'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Running integration tests on staging environment.'
                // Echo test results to a file
                sh 'echo "Integration Tests on Staging completed successfully." > integration_tests_staging_report.txt'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying the application to a production server.'
                // Echo deployment status to a file
                sh 'echo "Deployment to Production completed successfully." > deploy_production_report.txt'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
        }
    }
}



