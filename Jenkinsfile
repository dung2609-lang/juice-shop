pipeline {
  agent any

  tools {
    nodejs 'nodejs' // đúng với cấu hình NodeJS bạn đã tạo
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
        bat 'C:\\DevSecOps\\dependency-check\\bin\\dependency-check.bat --project "JuiceShop" --scan . --format HTML --out reports'
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
        bat 'zap-cli quick-scan --self-contained http://localhost:3000'
      }
    }
  }
}
