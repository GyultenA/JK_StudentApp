pipeline {
    agent any

    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Audit & Test in Parallel') {
            parallel {
                stage('Security Audit') {
                    steps {
                        bat 'npm audit'
                    }
                }

                stage('Run Tests') {
                    steps {
                        bat 'npm run test'
                    }
                }
            }
        }

    }

    post {
        always {
            echo 'Pipeline completed'
        }
        success {
            echo 'Build succeeded'
        }
        failure {
            echo 'Build failed'
        }
    }
}