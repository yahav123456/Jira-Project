pipeline {
    agent any
    
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm
            }
        }
    }
    
    post {
        always {
            script {
                def commitId = sh(script: 'git log -n 1 --pretty=format:%H', returnStdout: true).trim()
                def branchName = sh(script: "git branch --contains ${commitId} --format='%(refname:short)'", returnStdout: true).trim()
                echo "Branch Name: ${branchName}"
            }
        }
    }
}
