pipeline {
    agent any

    tools {
        nodejs 'Nodejs'
    }

    environment {
        NODE_ENV = 'production'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository to fetch the latest changes
                git 'https://github.com/codahal/project_test.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install dependencies
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                // Build the project
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Start or restart the specific PM2 process for project_test
                    sh '''
                    if pm2 describe project_test > /dev/null; then
                        pm2 restart project_test --env production
                    else
                        pm2 start ecosystem.config.js --env production --only project_test
                    fi
                    '''
                }
            }
        }
    }

    post {
        always {
            // List PM2 processes for debugging purposes
            sh 'pm2 list'
        }

        failure {
            // Print PM2 logs on failure
            sh 'pm2 logs'
        }
    }

    triggers {
        // GitHub webhook trigger
        githubPush()
    }
}

   
