pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git
                checkout scm
            }
        }

        stage('Get Branch Name') {
            steps {
                script {
                    // Extract branch name from Git environment variable
                    def branchName = env.BRANCH_NAME
                    echo "Merged branch name: ${branchName}"
                }
            }
        }
    }
}
