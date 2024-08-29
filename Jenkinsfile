pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/Users/lordram/Jenkins-pipeline'  // actual path
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'Ramesh-Prod'  // Using muy name as the production environment
    }

    stages {
        stage('Wait for a moment') {
            steps {
                script {
                    sleep(time: 30, unit: 'SECONDS') // Delays the pipeline by 30 seconds
                }
            }
        }

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts."
            }
        }
        
        stage('Test') {
            steps {
                echo 'Unit tests'
                echo 'Integration tests'
            }
        }

        stage('Code Quality Check') {
            steps {
                echo 'Check the quality of the code.'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy the application to the testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
            }
        }

        stage('Approval') {
            steps {
                echo 'Waiting for manual approval...'
                sleep time: 10, unit: 'SECONDS'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }
}
