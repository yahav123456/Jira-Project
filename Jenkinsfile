pipeline {
    agent any

    environment {
        // שם ה-branch בו עשינו merge
        MERGED_BRANCH_NAME = ""
        // הגדרת כתובת ה-Jira
        JIRA_SITE = 'jira'
    }

    stages {
        stage('Check Merge Branch') {
            steps {
                script {
                    // קריאה ל-git לקבל את שמות ה-branches הממוזגים ל-HEAD
                    def mergedBranch = sh(script: 'git branch -r --contains HEAD | grep -v HEAD | sed -n s/ *origin\\///p', returnStdout: true).trim()
                    // השמת שם ה-branch הממוזג במשתנה
                    MERGED_BRANCH_NAME = mergedBranch
                }
            }
        }

        stage('Change Jira Issue') {
            steps {
                script {
                    // שימוש ב-Issue ID כפי שהוגדר
                    def transitionInput = [
                        transition: [
                            id: '31'
                        ]
                    ]
                    // ביצוע פעולת ה-transition ב-Jira עבור ה-Issue המתאים ל-Issue ID
                    jiraTransitionIssue idOrKey: MERGED_BRANCH_NAME, input: transitionInput
                }
            }
        }
    }

    post {
        success {
            script {
                // שימוש ב-Issue ID כפי שהוגדר
                def transitionInput = [
                    transition: [
                        id: '31'
                    ]
                ]
                // ביצוע פעולת ה-transition ב-Jira עבור ה-Issue המתאים ל-Issue ID
                jiraTransitionIssue idOrKey: MERGED_BRANCH_NAME, input: transitionInput
            }
        }
    }
}
