pipeline {
  agent any
  stages {
    stage('git') {
      steps {
        git(url: 'https://github.com/MariiaMik/myJpetStore.git', branch: 'master', credentialsId: '103c120d19c8848aaef2b73010e5c644bb0c7af3')
      }
    }
  }
}