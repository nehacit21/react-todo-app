pipeline {
    agent any

    stages {
        stage('Stop Deployment') {
            steps {
                script {
                    // Stop the running deployment using pm2
                    sh 'pm2 stop react-todo-app'
                }
            }
        }

        stage('Pull Fresh Code') {
            steps {
                script {
                    // Navigate to the project directory
                    dir('/opt/checkout/react-todo-add') {
                        // Pull fresh code from Git
                        sh 'git clean -fd'  // Clean any untracked files and directories
                        sh 'git reset --hard HEAD'  // Discard changes in tracked files
                        sh 'git pull origin master'
                    }
                }
            }
        }

        stage('Build Project') {
            steps {
                script {
                    // Navigate to the project directory
                    dir('/opt/checkout/react-todo-add') {
                        // Install dependencies and build
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('Deploy using pm2') {
            steps {
                script {
                    // Move build files to deployment folder
                    sh 'cp -r /opt/checkout/react-todo-add/build/* /opt/deployment/react/'

                    // Start or restart the application using pm2
                    sh 'pm2 startOrRestart /opt/deployment/react/server.js --name react-todo-app'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
