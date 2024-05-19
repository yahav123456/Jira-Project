pipeline {
    agent any

    stages {
        stage('Send Branch Name to Jenkins') {
            steps {
                script {
                    // שליפת שם הבראנץ הנוכחי
                    def branchName = sh(script: 'git rev-parse --abbrev-ref HEAD', returnStdout: true).trim()

                    // שליחת שם הבראנץ הנוכחי ל Jenkins
                    echo "Branch Name: ${branchName}"
                }
            }
        }
    }
}
