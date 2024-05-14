pipeline {
  agent any
  stages {
    stage('for master branch') {
      when {
        branch 'master'
      }
      steps {
        echo 'master branch'
      }
    }
    stage('for stage branch') {
      when {
        branch 'master-staging'
      }
      steps {
        echo 'stage branch: Deploying changes to master'
        git branch: 'master-staging', url: 'https://github.com/bill-keplar/multibranch-pipeline-project.git'
        sh 'git fetch'
        sh 'git checkout -b master origin/master && git pull && git rebase master-staging && git push origin master'
      }
    }
    stage('for pull request') {
      when {
        changeRequest()
      }
      steps {
        echo 'pull request'
      }
    }
  }
}