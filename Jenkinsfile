pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                echo 'Lấy code từ Git...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Đang build OWASP Juice Shop...'
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Chạy test...'
                bat 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Triển khai ứng dụng hoàn tất!'
            }
        }
    }
}
