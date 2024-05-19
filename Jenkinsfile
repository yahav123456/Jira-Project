pipeline {
    agent any

    stages {
        stage('Get Last Merged Branch') {
            steps {
                script {
                    def lastMergedBranch = sh(script: 'git branch --merged main --format="%(refname:short)" | grep -v "main" | head -1', returnStdout: true).trim()
                    echo "Last Merged Branch: ${lastMergedBranch}"
                    
                    writeFile file: 'last_merged_branch.properties', text: "LAST_MERGED_BRANCH=${lastMergedBranch}"
                }
            }
        }
    }
}
