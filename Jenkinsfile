node {
  stage('JIRA') {
    // הנח שהשם של ה-branch שממנו נעשה merge נשמר כ-BRANCH_NAME
    def branchName = env.BRANCH_NAME

    withEnv(['JIRA_SITE=jira']) {
      def transitionInput =
      [
          transition: [
              id: '31'
          ]
      ]

      // משתמש בשם ה-branch כ-ID של ה-issue
      jiraTransitionIssue idOrKey: branchName, input: transitionInput
    }
  }
}
