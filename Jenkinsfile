pipeline {
    agent any

    stages {
        stage('Wait for a moment') {
            steps {
                script {
                    sleep(time: 30, unit: 'SECONDS') // Delays the pipeline by 30 seconds
                }
            }
        }

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
                    mail to: "rameshkavinda95@gmail.com",
                    subject: "Unit and Integration Tests status",
                    body: "The Unit and Integration Tests stage has completed successfully!"
                }
                failure {
                    mail to: "rameshkavinda95@gmail.com",
                    subject: "Unit and Integration Tests status",
                    body: "The Unit and Integration Tests stage has failed!"
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
                    mail to: "rameshkavinda95@gmail.com",
                    subject: "Security Scan status",
                    body: "The Security Scan stage has completed successfully!"
                }
                failure {
                    mail to: "rameshkavinda95@gmail.com",
                    subject: "Security Scan status",
                    body: "The Security Scan stage has failed!"
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
