pipeline {
    agent any

    stages {
        stage('Check Merge Branch') {
            steps {
                script {
                    // מציאת שם ה-branch מפעולת ה-merge ב-Git
                    def branchName = env.GIT_BRANCH
                    // הדפסת שם ה-branch לצורך בדיקה
                    echo "Merged branch name: ${branchName}"
                    // כאן תוכל להוסיף פעולות נוספות על פי הצורך
                }
            }
        }
    }
}
