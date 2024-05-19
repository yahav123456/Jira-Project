pipeline {
    agent any

    environment {
        // שמירת שם ה-branch במשתנה
        GIT_BRANCH_NAME = "${env.GIT_BRANCH}"
        // הגדרת כתובת ה-Jira
        JIRA_SITE = 'jira'
    }

    stages {
        stage('Change Jira Issue') {
            steps {
                script {
                    // קריאה ל-git לקבל את שמות ה-branches
                    def branchName = env.GIT_BRANCH_NAME
                    // חיתוך ה-Issue ID משם ה-branch
                    def issueID = branchName.split('/')[1]

                    // שימוש ב-Issue ID כפי שהוגדר
                    def transitionInput = [
                        transition: [
                            id: '31'
                        ]
                    ]
                    // ביצוע פעולת ה-transition ב-Jira עבור ה-Issue המתאים ל-Issue ID
                    jiraTransitionIssue idOrKey: issueID, input: transitionInput
                }
            }
        }
    }

    post {
        success {
            script {
                // קריאה ל-git לקבל את שמות ה-branches
                def branchName = env.GIT_BRANCH_NAME
                // חיתוך ה-Issue ID משם ה-branch
                def issueID = branchName.split('/')[1]

                // שימוש ב-Issue ID כפי שהוגדר
                def transitionInput = [
                    transition: [
                        id: '31'
                    ]
                ]
                // ביצוע פעולת ה-transition ב-Jira עבור ה-Issue המתאים ל-Issue ID
                jiraTransitionIssue idOrKey: issueID, input: transitionInput
            }
        }
    }
}
