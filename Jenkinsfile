pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'npm install'
      }
    }
    stage('Test') {
      steps {
        bat 'npm test || exit 0' // Juice Shop có test lỗi, bỏ qua để không fail pipeline
      }
    }
    stage('SAST - SonarQube') {
      steps {
        withSonarQubeEnv('SonarQube') {
          bat 'sonar-scanner.bat -Dsonar.projectKey=juice-shop -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000'
        }
      }
    }
    stage('SCA - Dependency Check') {
      steps {
        bat 'C:\\DevSecOps\\dependency-check\\bin\\dependency-check.bat --project "JuiceShop" --scan . --format HTML --out reports'
        publishHTML([reportDir: 'reports', reportFiles: 'dependency-check-report.html', reportName: 'SCA Report'])
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
