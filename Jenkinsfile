pipeline {
    agent any

    stages {
        stage('זיהוי שם ה-Branch האחרון') {
            steps {
                // קבלת שם ה-Commit האחרון ב-Branch "main"
                script {
                    def mainBranchCommit = sh(script: "git rev-parse HEAD^1 main", returnStdout: true).trim()
                    echo "שם ה-Commit האחרון ב-Branch 'main': ${mainBranchCommit}"

                    // קבלת שם ה-Branch מה-Commit האחרון
                    def branchName = sh(script: "git branch --contains ${mainBranchCommit} | head -1 | sed 's/remotes/origin\/HEAD -> //'", returnStdout: true).trim()
                    echo "שם ה-Branch האחרון שמוזג ל-Main: ${branchName}"

                    // הגדרת משתנה סביבה עם שם ה-Branch
                    env.BRANCH_NAME = branchName
                }
            }
        }
    }
}
