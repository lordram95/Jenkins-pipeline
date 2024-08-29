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
                    writeFile file: 'test-results.log', text: 'Test results log content...'   
                }
            }
            post {
                always {
                    script {
                        if (fileExists('test-results.log')) {
                            emailext(
                                subject: "Unit and Integration Tests Completed: ${currentBuild.currentResult}",
                                body: "The Unit and Integration Tests stage has completed with status: ${currentBuild.currentResult}.",
                                to: 's223987441@deakin.edu.au',
                                attachmentsPattern: 'test-results.log'
                            )
                        } else {
                            echo 'Test log file not found.'
                        }
                    }
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
                    writeFile file: 'security-scan.log', text: 'Security scan log content...'
                }
            }
            post {
                always {
                    script {
                        if (fileExists('security-scan.log')) {
                            emailext(
                                subject: "Security Scan Completed: ${currentBuild.currentResult}",
                                body: "The Security Scan stage has completed with status: ${currentBuild.currentResult}.",
                                to: 's223987441@deakin.edu.au',
                                attachmentsPattern: 'security-scan.log'
                            )
                        } else {
                            echo 'Security scan log file not found.'
                        }
                    }
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
