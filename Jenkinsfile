pipeline {
    agent any

    triggers {
        scm 
    }

    stages {
        stage('זיהוי שם ה-Branch האחרון') {
            steps {
                script {
                    // קבלת שם ה-Commit האחרון ב-Branch "main"
                    def mainBranchCommit = sh(script: "git rev-parse origin/main", returnStdout: true).trim()
                    echo "שם ה-Commit האחרון ב-Branch 'main': ${mainBranchCommit}"

                    // קבלת שם ה-Branch מה-Commit האחרון
                    def branchName = sh(script: "git branch --contains ${mainBranchCommit} | head -1 | sed 's/remotes\\/origin\\///'", returnStdout: true).trim()
                    echo "שם ה-Branch האחרון שמוזג ל-Main: ${branchName}"

                    // הגדרת משתנה סביבה עם שם ה-Branch
                    env.BRANCH_NAME = branchName
                }
            }
        }
    }
}
