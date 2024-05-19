pipeline {
    agent any

    stages {
        stage('Send Branch Name to Jenkins') {
            steps {
                script {
                    // שליפת שם הבראנץ ממשתנה הסביבה GIT_BRANCH
                    def branchName = env.GIT_BRANCH
                    // ניקוי שם הבראנץ מתווים נוספים
                    branchName = branchName.replaceAll('origin/', '')
                    // שליחת שם הבראנץ ל Jenkins
                    echo "Branch Name: ${branchName}"
                }
            }
        }
    }
}
