pipeline {
  agent any
  stages {
    stage('git') {
      steps {
        git(url: 'https://github.com/MariiaMik/myJpetStore.git', branch: 'master', credentialsId: 'github')
      }
    }
    stage('maven') {
      steps {
        bat(encoding: 'utf-8', script: 'runmaven.bat')
      }
    }
    stage('sonar') {
      steps {
        withSonarQubeEnv('My SonarQube Server') {
          bat(encoding: 'utf-8', script: 'runsonar.bat')
        }
      }
    }
    stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
    stage('nexus') {
      steps {
        nexusArtifactUploader(nexusVersion: 'nexus3', protocol: 'http', nexusUrl: 'localhost:8081/', groupId: 'jpetstore', version: '1.0-SNAPSHOT', repository: 'maven-snapshots', credentialsId: 'nexus3', artifacts: [
                                                                      					[artifactId: 'jpetstore',
                                                                      					 classifier: 'debug',
                                                                      					 file: 'target/jpetstore.war',
                                                                      					 type: 'war']
                                                                      				])
        }
      }
    }
  }
