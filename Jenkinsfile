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
                echo 'Cài đặt phụ thuộc...'
                bat 'npm install || echo "npm install skipped"'
            }
        }

        stage('Test') {
            steps {
                echo 'Chạy kiểm thử giả lập...'
                bat 'echo "No tests - Skip"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Triển khai hoàn tất (mô phỏng)...'
            }
        }
    }
}
