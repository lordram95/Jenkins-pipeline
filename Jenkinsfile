pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    echo 'Tool: Maven'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running Unit and Integration Tests...'
                    echo 'Tools: JUnit, TestNG'
                }
            }
            post {
                success {
                    emailext (
                        to: "rameshkavinda95@gmail.com",
                        subject: "Unit and Integration Tests Status - Success",
                        body: "The Unit and Integration Tests stage has completed successfully!",
                        attachmentsPattern: '**/build.log'
                    )
                }
                failure {
                    emailext (
                        to: "rameshkavinda95@gmail.com",
                        subject: "Unit and Integration Tests Status - Failure",
                        body: "The Unit and Integration Tests stage has failed!",
                        attachmentsPattern: '**/build.log'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing Code Analysis...'
                    echo 'Tool: SonarQube'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing Security Scan...'
                    echo 'Tool: OWASP Dependency-Check'
                }
            }
            post {
                success {
                    emailext (
                        to: "rameshkavinda95@gmail.com",
                        subject: "Security Scan Status - Success",
                        body: "The Security Scan stage has completed successfully!",
                        attachmentsPattern: '**/security_scan.log'
                    )
                }
                failure {
                    emailext (
                        to: "rameshkavinda95@gmail.com",
                        subject: "Security Scan Status - Failure",
                        body: "The Security Scan stage has failed!",
                        attachmentsPattern: '**/security_scan.log'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to Staging...'
                    echo 'Server: AWS EC2 Instance'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running Integration Tests on Staging...'
                    echo 'Tools: JUnit, Selenium'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to Production...'
                    echo 'Server: AWS EC2 Instance'
                }
            }
        }
    }
}
