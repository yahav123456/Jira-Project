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
                    // קריאה ל-git לקבל את שמות ה-branches שמוזגו
                    def branches = sh(script: 'git branch --merged', returnStdout: true).trim()
                    // סידור התוצאות ופילטרים
                    def branchList = branches.tokenize('\n').collect { it.trim() }
                        .findAll { it != '*' && it != 'master' && it != 'main' }

                    // בדיקה האם קיים רק branch אחד שממנו נעשה merge
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
            when {
                // רק כאשר שם ה-branch שממנו נעשה merge אינו ריק
                expression { MERGED_BRANCH_NAME != '' }
            }
            steps {
                script {
                    // בדיקה שהמשתנה MERGED_BRANCH_NAME לא ריק
                    if (MERGED_BRANCH_NAME) {
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
    }

    post {
        success {
            script {
                // בדיקה שהמשתנה MERGED_BRANCH_NAME לא ריק
                if (MERGED_BRANCH_NAME) {
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
}
