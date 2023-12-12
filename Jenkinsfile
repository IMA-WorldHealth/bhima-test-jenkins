pipeline {
  agent any

  triggers {
    cron '''0 * * * *
  '''
  }

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
      archiveArtifacts artifacts: 'results.zip, results/summary.txt', fingerprint: true
      junit skipPublishingChecks: true, testResults: 'results/*.xml'
    }

    changed {
      mail to: 'bhima@jmcameron.net', 
      subject: 'BHIMA End-to-end Tests Regression: ${currentBuild.fullDisplayName}',
      from: 'noreply+bhima@jmcameron.net', 
      body: "Details: ${env.JOB_NAME} Build Number: ${env.BUILD_NUMBER} Build: ${env.BUILD_URL} Console Output: ${env.BUILD_URL}/console"
    }

    failure {  
      mail to: 'bhima@jmcameron.net', 
      subject: 'BHIMA End-to-end Tests Failure: ${currentBuild.fullDisplayName}',
      from: 'noreply+bhima@jmcameron.net', 
      body: "Details: ${env.JOB_NAME} Build Number: ${env.BUILD_NUMBER} Build: ${env.BUILD_URL} Console Output: ${env.BUILD_URL}/console"
    }  

  }
}
