pipeline {
  agent any

  tools {
    nodejs 'nodejs'
  }

  stages {
    stage('Build') {
      steps {
        bat 'npm install --legacy-peer-deps'
      }
    }

    stage('Test') {
      steps {
        bat 'echo "Skipping frontend tests (karma not used)"'
      }
    }

    stage('SCA - Dependency Check') {
      steps {
        bat 'npm install --package-lock-only'
        script {
          def result = bat(
            script: '''
              C:\\DevSecOps\\dependency-check\\bin\\dependency-check.bat ^
              --project "JuiceShop" ^
              --scan . ^
              --format HTML ^
              --out reports ^
              --disableArchive ^
              --disableOssIndex ^
              --disableYarnAudit ^
              --exclude "**/dist/**" ^
              --exclude "**/ftp/**"
            ''',
            returnStatus: true
          )
          echo "Dependency Check exited with code ${result}"
        }
        publishHTML([
          reportDir: 'reports',
          reportFiles: 'dependency-check-report.html',
          reportName: 'SCA Report',
          allowMissing: false,
          alwaysLinkToLastBuild: true,
          keepAll: true
        ])
      }
    }

    stage('Deploy') {
      steps {
        bat 'start /B npm start'
      }
    }

    stage('DAST - OWASP ZAP') {
      steps {
        bat 'echo "Skipping ZAP scan (zap-cli not installed)"'
      }
    }
  }
}
