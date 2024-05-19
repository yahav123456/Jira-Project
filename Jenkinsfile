pipeline {
    agent any

    triggers {
        scm * // הפעלת ה-Pipeline בכל Push ל-Git
    }

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

                    // בדיקה אם שם ה-Branch תואם את פרויקט 6
                    if (branchName.contains("PROJ-6")) {
                        echo "ה-Branch שמוזג ל-Main הוא פרויקט 6!"
                    } else {
                        echo "ה-Branch שמוזג ל-Main אינו פרויקט 6."
                    }
                }
            }
        }
    }
}
