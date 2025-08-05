pipeline {
  agent any

  tools {
    nodejs 'Node 20'
  }

  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test & Coverage') {
      steps {
        sh 'npm run coverage'
      }
    }

    stage('Publish HTML') {
      steps {
        publishHTML(target: [
          allowMissing: false,
          alwaysLinkToLastBuild: true,
          keepAll: true,
          reportDir: 'coverage',
          reportFiles: 'index.html',
          reportName: 'Coverage Report'
        ])
      }
    }

    stage('Publish Cobertura') {
      steps {
        cobertura coberturaReportFile: 'coverage/cobertura-coverage.xml'
      }
    }
  }
}
