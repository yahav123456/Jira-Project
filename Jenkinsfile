pipeline {
    agent any

    environment {
        // שמירת שם ה-branch במשתנה
        GIT_BRANCH_NAME = "${env.GIT_BRANCH}"
        // קיצוץ ה-"origin/" משם ה-branch
        ISSUE_ID = GIT_BRANCH_NAME.replaceAll('origin/', '')
        // הגדרת כתובת ה-Jira
        JIRA_SITE = 'jira'
    }

    stages {
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
                    jiraTransitionIssue idOrKey: ISSUE_ID, input: transitionInput
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
                jiraTransitionIssue idOrKey: ISSUE_ID, input: transitionInput
            }
        }
    }
}
