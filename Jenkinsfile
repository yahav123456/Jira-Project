pipeline {
    agent any

    stages {
        stage('Get Branch Name') {
            steps {
                script {
                    // בדיקה אם המשתנה GIT_BRANCH קיים ומכיל מידע
                    def branchName = env.GIT_BRANCH ? env.GIT_BRANCH : sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                    echo "Branch Name: ${branchName}"
                    env.BRANCH_NAME = branchName
                }
            }
        }

        stage('JIRA') {
            steps {
                script {
                    withEnv(['JIRA_SITE=jira']) {
                        def transitionInput = [
                            transition: [
                                id: '31'
                            ]
                        ]

                        // משתמש בשם ה-branch כ-ID של ה-issue
                        echo "Transitioning JIRA issue: ${env.BRANCH_NAME}"
                        jiraTransitionIssue idOrKey: env.BRANCH_NAME, input: transitionInput
                    }
                }
            }
        }
    }
}
