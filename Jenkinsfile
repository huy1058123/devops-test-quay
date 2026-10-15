pipeline {
    agent any

    environment {
        TELEGRAM_TOKEN = '8915966334:AAHp5GXz0i2SlrW3bcu8znhfNRhcnIZKBrk'
        CHAT_ID = '7627383909'
        PROJECT_NAME = 'devops-test'
        BRANCH_NAME = 'main'
        WEBSITE_URL = 'http://localhost'
    }

    stages {
        stage('Deploy Started Notification') {
            steps {
                script {
                    bat """
                    curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage" -d "chat_id=${CHAT_ID}" -d "text=🚀 DEPLOY STARTED%0AProject: ${PROJECT_NAME}%0ABranch: ${BRANCH_NAME}"
                    """
                }
            }
        }

        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
            }
        }

        stage('Build Project') {
            steps {
                echo 'Building project...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to web server...'
            }
        }
    }

    post {
        success {
            script {
                bat """
                curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage" -d "chat_id=${CHAT_ID}" -d "text=✅ DEPLOY SUCCESS NHÉ%0AProject: ${PROJECT_NAME}%0ABranch: ${BRANCH_NAME}%0AURL: ${WEBSITE_URL}"
                """
            }
        }
        failure {
            script {
                bat """
                curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage" -d "chat_id=${CHAT_ID}" -d "text=❌ DEPLOY FAILED RỒI%0AProject: ${PROJECT_NAME}%0ABranch: ${BRANCH_NAME}%0APlease check Jenkins."
                """
            }
        }
    }
}