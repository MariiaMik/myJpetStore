pipeline {
  agent any
  stages {
    stage('git') {
      steps {
        git(url: 'https://github.com/MariiaMik/myJpetStore.git', branch: 'master', credentialsId: '103c120d19c8848aaef2b73010e5c644bb0c7af3')
      }
    }
    stage('maven') {
      steps {
        bat(encoding: 'utf-8', script: 'runmaven.bat')
      }
    }
    stage('nexus') {
      steps {
        nexusArtifactUploader(nexusVersion: 'nexus3', protocol: 'http', nexusUrl: 'localhost:8081', groupId: 'jpetstore', version: '1.0', repository: 'maven-snapshots', credentialsId: 'nexus3', artifacts: [
          					[artifactId: jpetstore,
          					 classifier: '',
          					 file: 'target/jpetstore-' + version + '.war',
          					 type: 'war']
          				])
        }
      }
    }
  }