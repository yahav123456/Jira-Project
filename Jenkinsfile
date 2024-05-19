pipeline {
    agent any

    environment {
        GIT_BRANCH_NAME = "${env.GIT_BRANCH}" // לשמור את שם ה-branch
        JIRA_SITE = 'jira' // הוספת הגדרה זו
    }

    stages {
        stage('Change Jira Issue') {
            steps {
                script {
                    // הסרת 'origin/' אם קיים בשם ה-branch
                    def issueId = GIT_BRANCH_NAME.replaceAll('origin/', '')
                    
                    // שינוי סטטוס ה-issue ב-Jira באמצעות מזהה מעבר
                    def transitionInput = [
                        transition: [
                            id: '31'
                        ]
                    ]
                    jiraTransitionIssue idOrKey: issueId, input: transitionInput
                }
            }
        }
    }

    post {
        success {
            script {
                // שוב הסרת 'origin/' אם קיים בשם ה-branch לשימוש לאחר הצלחת הפייפליין
                def issueId = GIT_BRANCH_NAME.replaceAll('origin/', '')
                
                // שינוי סטטוס ה-issue ב-Jira באמצעות מזהה מעבר לאחר הצלחת הפייפליין
                def transitionInput = [
                    transition: [
                        id: '31'
                    ]
                ]
                jiraTransitionIssue idOrKey: issueId, input: transitionInput
            }
        }
    }
}
