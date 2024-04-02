pipeline {
    agent any

    stages {
        stage('Check Queue and Abort') {
            steps {
                script {
                    def queue = Jenkins.instance.queue
                    if (queue.isEmpty()) {
                        echo "No builds queued, proceeding with the current build"
                    } else {
                        echo "A build is queued, aborting the current build"
                        currentBuild.result = 'ABORTED'
                        error "Build aborted due to a queued build"
                    }
                }
            }
        }
        stage('Build') {
            steps {
                // Your build steps here
                echo "Building..."
                // For example, npm start
                sh 'npm start'
            }
        }
    }
}