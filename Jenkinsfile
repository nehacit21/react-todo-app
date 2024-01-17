pipeline {
    agent any

    tools {
        nodejs 'nodejs'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    sh 'npm install'
                    sh 'npm test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Your deployment steps here
                    // For example, you can use pm2 to start the app
                    sh 'npm install -g pm2'
                    sh 'pm2 start server.js'
                }
            }
        }
    }
}
