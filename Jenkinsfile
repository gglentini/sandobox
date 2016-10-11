node(labels['scm']) {
    def clazz

    timestamps() {
        stage('Delete the workspace before the run')
            sh 'rm -rf ./*'

        stage('Clone the code')
            // clone the repository
            git branch: helpersBranchName, changelog: false, poll: false, url: helpersRepoUrl
            if (refspec) {
                // if refspec is defined, the job has been triggered by Gerrit,
                // so we need to pull the change in review
                // otherwise, stick to the current HEAD cloned above
                sh "git fetch ${helpersRepoUrl} ${refspec}"
                sh 'git checkout FETCH_HEAD'
            }
    }
}
