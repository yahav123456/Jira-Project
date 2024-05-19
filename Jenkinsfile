pipeline {
    agent any

    stages {
        stage('Send Branch Name to Jenkins') {
            steps {
                script {
                    // שליפת שמות הבראנצ'ים המושפעים מהcommit האחרון
                    def branches = sh(script: 'git branch -r --contains HEAD | grep -v HEAD | cut -d \'/\' -f 2', returnStdout: true).trim()
                    // ניתוב הפלט לתוך מערך
                    def branchList = branches.tokenize('\n').collect { it.trim() }

                    // הדפסת רשימת הבראנצ'ים לצורך בדיקה
                    echo "Branches: ${branchList}"

                    // שליחת שם הבראנץ האחרון ל Jenkins
                    echo "Branch Name: ${branchList.last()}"
                }
            }
        }
    }
}
