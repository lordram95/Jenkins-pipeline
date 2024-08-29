pipeline {
    agent any

    environment {
        BUILD_LOG = 'build.log'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    echo 'Tool: Maven'
                    // Run Maven and redirect output to build.log
                    sh 'mvn clean install > ${BUILD_LOG} 2>&1'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running Unit and Integration Tests...'
                    echo 'Tools: JUnit, TestNG'
                    // Run tests and append output to build.log
                    sh 'mvn test >> ${BUILD_LOG} 2>&1'
                }
            }
            post {
                always {
                    emailext (
                        to: "rameshkavinda95@gmail.com",
                        subject: "Unit and Integration Tests status - ${currentBuild.currentResult}",
                        body: "The Unit and Integration Tests stage has ${currentBuild.currentResult.toLowerCase()}! Check the build logs for details.",
                        attachmentsPattern: "${BUILD_LOG}"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing Code Analysis...'
                    echo 'Tool: SonarQube'
                    // Run code analysis and append output to build.log
                    sh 'sonar-scanner >> ${BUILD_LOG} 2>&1'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing Security Scan...'
                    echo 'Tool: OWASP Dependency-Check'
                    // Run security scan and append output to build.log
                    sh 'dependency-check.sh >> ${BUILD_LOG} 2>&1'
                }
            }
            post {
                always {
                    emailext (
                        to: "rameshkavinda95@gmail.com",
                        subject: "Security Scan status - ${currentBuild.currentResult}",
                        body: "The Security Scan stage has ${currentBuild.currentResult.toLowerCase()}! Check the build logs for details.",
                        attachmentsPattern: "${BUILD_LOG}"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to Staging...'
                    echo 'Server: AWS EC2 Instance'
                    // Run staging deployment and append output to build.log
                    sh 'deploy-to-staging.sh >> ${BUILD_LOG} 2>&1'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running Integration Tests on Staging...'
                    echo 'Tools: JUnit, Selenium'
                    // Run integration tests and append output to build.log
                    sh 'mvn integration-test >> ${BUILD_LOG} 2>&1'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to Production...'
                    echo 'Server: AWS EC2 Instance'
                    // Run production deployment and append output to build.log
                    sh 'deploy-to-production.sh >> ${BUILD_LOG} 2>&1'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: "${BUILD_LOG}", allowEmptyArchive: true
        }
    }
}
