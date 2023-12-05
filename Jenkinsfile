pipeline {
  agent any
  stages {
    stage('Start E2E Tests') {
      agent any
      steps {
        echo 'Starting'
      }
    }

    stage('Run remote E2E tests') {
      steps {
        sh '''/home/jenkins/builds/run_tests'''
      }
    }

  }

  post {
    always { 
      archiveArtifacts artifacts: 'builds/Bhima/results.zip', fingerprint: true
      junit '../builds/Bhima/results/*.xml'
    }
  }
}
