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
        always {
            echo 'Pipeline completed.'
        }
    }
}

