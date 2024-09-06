pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                echo 'Using build tool: Maven'
                sh 'echo "Build log contents" > build-log.txt'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Using test tools: JUnit (Java), Mocha (Node.js)'
                sh 'echo "Unit and integration test log contents" > test-log.txt'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/test-logs/*.log', allowEmptyArchive: true
                }
                success {
                    sendEmail(
                        stageName: 'Unit and Integration Tests',
                        stageStatus: 'SUCCESS',
                        attachmentsPattern: '**/test-logs/*.log'
                    )
                }
                failure {
                    sendEmail(
                        stageName: 'Unit and Integration Tests',
                        stageStatus: 'FAILURE',
                        attachmentsPattern: '**/test-logs/*.log'
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                echo 'Using code analysis tool: SonarQube'
                sh 'echo "Code analysis log contents" > code-analysis-log.txt'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                echo 'Using security scan tool: Snyk'
                sh 'echo "Security scan log contents" > security-scan-log.txt'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/security-logs/*.log', allowEmptyArchive: true
                }
                success {
                    sendEmail(
                        stageName: 'Security Scan',
                        stageStatus: 'SUCCESS',
                        attachmentsPattern: '**/security-logs/*.log'
                    )
                }
                failure {
                    sendEmail(
                        stageName: 'Security Scan',
                        stageStatus: 'FAILURE',
                        attachmentsPattern: '**/security-logs/*.log'
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
        always {
            archiveArtifacts artifacts: '**/*.txt', onlyIfSuccessful: true
            emailext (
                subject: "Jenkins Build Report ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n Link: ${env.BUILD_URL}",
                to: "work.kadyan@gmail.com",
                attachmentsPattern: '**/*.txt',
                replyTo: "work.kadyan@gmail.com",
                compressLog: true,
                attachLog: true
            )
        }
    }
}

// Helper function to send emails with stage status
def sendEmail(Map params) {
    emailext (
        subject: "Stage ${params.stageName} ${params.stageStatus}: Job ${env.JOB_NAME}",
        body: "The ${params.stageName} stage has ${params.stageStatus}. Please review the attached logs.\n\nLink: ${env.BUILD_URL}",
        to: "work.kadyan@gmail.com",
        attachmentsPattern: params.attachmentsPattern,
        replyTo: "work.kadyan@gmail.com",
        compressLog: true
    )
}



