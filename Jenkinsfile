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
        stage('Deploy') {
            steps {
                input message: 'Approve deployment?', ok: 'Deploy'
                bat 'echo Deploying application..' // replace with real deploy command
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