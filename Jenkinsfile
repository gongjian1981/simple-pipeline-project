pipeline {
  agent any

  tools {
    nodejs 'Node 20' // Make sure you configured this in Jenkins global tools
  }

  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Test & Coverage') {
      steps {
        sh 'npm run coverage'
      }
    }

    stage('Publish HTML Report') {
      steps {
        publishHTML(target: [
          allowMissing: false,
          alwaysLinkToLastBuild: true,
          keepAll: true,
          reportDir: 'coverage',
          reportFiles: 'index.html',
          reportName: 'Jest Coverage Report'
        ])
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'coverage/**/*.*', onlyIfSuccessful: true
    }
  }
}
