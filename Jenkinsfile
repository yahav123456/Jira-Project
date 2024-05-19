pipeline {
    agent any

    triggers {
        scm 
    }

    stages {
        stage('זיהוי שם ה-Branch האחרון') {
            steps {
                script {
                    echo "מתחיל בקריאה ל־GitHub לשם ה־branch"

                    // קבלת שם ה-Commit האחרון ב-Branch "main"
                    def mainBranchCommit = sh(script: "git rev-parse origin/main", returnStdout: true).trim()
                    echo "שם ה-Commit האחרון ב-Branch 'main': ${mainBranchCommit}"

                    // קבלת שם ה-Branch מה-Commit האחרון
                    def branchName = sh(script: "git branch --contains ${mainBranchCommit} | head -1 | sed 's/remotes\\/origin\\///'", returnStdout: true).trim()
                    echo "שם ה-Branch האחרון שמוזג ל-Main: ${branchName}"

                    // הגדרת משתנה סביבה עם שם ה-Branch
                    env.BRANCH_NAME = branchName

                    echo "סיים בקריאה ל־GitHub לשם ה־branch"

                    // Checkout מה־GitHub
                    echo "בוצע Checkout מה־GitHub"
                    checkout scm
                    echo "סיים Checkout מה־GitHub"
                }
            }
        }

        stage('JIRA') {
            when {
                expression { env.BRANCH_NAME != null }
            }
            steps {
                echo "שם ה-Branch שמוזג ל-Main הוא: ${env.BRANCH_NAME}"

                withEnv(['JIRA_SITE=jira']) {
                    def transitionInput =
                    [
                        transition: [
                            id: '31'
                        ]
                    ]

                    // שימוש בשם ה־branch כחלק משם ה־issue ב־Jira
                    def issueName = env.BRANCH_NAME.toUpperCase() // לדוגמה, שימוש בשם ה־branch באותיות גדולות
                    jiraTransitionIssue idOrKey: issueName, input: transitionInput
                }
            }
        }
    }
}
