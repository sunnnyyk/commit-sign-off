pipeline {
    agent any
    environment {
        PROJECT_REPO = 'https://github.com/OT-MICROSERVICES/notification-worker.git'
        PROJECT_BRANCH = 'main'
    }
    stages {
        stage('Checkout Project') {
            steps {
                git branch: "${PROJECT_BRANCH}", url: "${PROJECT_REPO}"
            }
        }

        stage('Check Commit Sign-off') {
            steps {
                script {
                    def lastCommitMessage = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()
                    if (!lastCommitMessage.contains("Signed-off-by:")) {
                        error("The latest commit is missing 'Signed-off-by:'. Build failed.")
                    } else {
                        echo "Commit sign-off verified."
                    }
                }
            }
        }
    }
}
