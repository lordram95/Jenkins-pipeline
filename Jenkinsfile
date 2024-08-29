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
                always {
                    mail to: 's223987441@deakin.edu.au',
                         subject: "Unit and Integration Tests Completed: ${currentBuild.currentResult}",
                         body: "The tests have completed with status: ${currentBuild.currentResult}.\n\nLogs:\n${testLog}"
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
                always {
                    mail to: 's223987441@deakin.edu.au',
                         subject: "Security Scan Completed: ${currentBuild.currentResult}",
                         body: "The security scan has completed with status: ${currentBuild.currentResult}.\n\nLogs:\n${securityLog}"
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

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
