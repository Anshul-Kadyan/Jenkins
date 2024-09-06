
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
                script {
                    // Capture output for Unit and Integration Tests stage
                    def testOutput = sh(script: 'echo "Running unit and integration tests..."', returnStdout: true).trim()
                    writeFile file: 'unit_test_log.txt', text: testOutput
                }
            }
            post {
                always {
                    // Send email with logs attached for the Unit and Integration Tests stage
                    emailext(
                        to: 'work.kadyan@gmail.com',
                        subject: "Unit and Integration Tests Status: ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests have finished with status: ${currentBuild.currentResult}.",
                        attachmentsPattern: 'unit_test_log.txt'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                echo 'Using analysis tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    // Capture output for Security Scan stage
                    def securityOutput = sh(script: 'echo "Performing security scan..."', returnStdout: true).trim()
                    writeFile file: 'security_scan_log.txt', text: securityOutput
                }
            }
            post {
                always {
                    // Send email with logs attached for the Security Scan stage
                    emailext(
                        to: 'work.kadyan@gmail.com',
                        subject: "Security Scan Status: ${currentBuild.currentResult}",
                        body: "The Security Scan has finished with status: ${currentBuild.currentResult}.",
                        attachmentsPattern: 'security_scan_log.txt'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                echo 'Deploying to staging using AWS EC2'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
                echo 'Using testing tool: JUnit'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                echo 'Deploying to production using AWS EC2'
            }
        }
    }
    post {
    success {
        emailext (
            subject: "Build Success",
            body: "The build was successful.",
            to: "work.kadyan@gmail.com"
        )
    }
    failure {
        emailext (
            subject: "Build Failure",
            body: "The build failed.",
            to: "work.kadyan@gmail.com"
        )
    }
}

}
