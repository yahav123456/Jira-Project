pipeline {
    agent any

    environment {
        // שמירת שם ה-branch במשתנה
        GIT_BRANCH_NAME = "${env.GIT_BRANCH}"
        // שם ה-branch בו עשינו merge
        MERGED_BRANCH_NAME = ""
        // הגדרת כתובת ה-Jira
        JIRA_SITE = 'jira'
    }

    stages {
        stage('Check Merge Branch') {
            steps {
                script {
                    // קריאה ל-git לקבל את שמות ה-branches
                    def branches = sh(script: 'git branch --merged', returnStdout: true).trim()
                    // סידור התוצאות ופילטרים
                    def branchList = branches.tokenize('\n').collect { it.trim() }
                        .findAll { it != '*' && it != 'master' && it != 'main' }

                    // המציאות בה נעשה merge מאפשרת רק ענפים אחרים
                    if (branchList.size() == 1) {
                        // השמת שם ה-branch הממנו עשינו merge במשתנה
                        MERGED_BRANCH_NAME = branchList[0]
                    } else {
                        // אם יש יותר מענף אחד, יש לבחור כיצד לטפל
                        // כאן אפשר להוסיף לוגיקה למצבים נוספים אם נדרש
                        error("More than one branch merged, handle this case.")
                    }
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
