pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Check Merge Branch') {
            steps {
                script {
                    // שליפת שם הבראנץ מההיסטוריה של הקומיטים
                    def mergedBranch = sh(script: 'git branch -r --contains HEAD | grep -v HEAD | sed -n \'s/ *origin\\///p\'', returnStdout: true).trim()
                    
                    // הצגת הבראנץ שהושג
                    echo "Merged branch name: ${mergedBranch}"
                    
                    // בדיקה אם התקבל שם של בראנץ
                    if (mergedBranch) {
                        // עריכת הפעולות שלאחרי הבדיקה
                    } else {
                        error "Failed to determine merged branch name."
                    }
                }
            }
        }
        
        // הוספת שלבים נוספים כפי שנדרש...
    }
    
    // הוספת מצבי סיום כפי שנדרש...
}
