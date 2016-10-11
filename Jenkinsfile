// Repository and branch where the code is saved
def helpersRepoUrl = 'https://github.com/gglentini/sandobox.git'
// if the job is triggered by Gerrit, get the branch received as parameter,
// otherwise fallback to the current development branch 'master'
def helpersBranchName = GERRIT_BRANCH ? GERRIT_BRANCH : 'master'

// the Gerrit refspec where the code we want to test is saved,
// received as a build parameter
def refspec = GERRIT_REFSPEC

node('scm') {
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
