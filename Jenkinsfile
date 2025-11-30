pipeline {
    agent any

    environment {
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-21" // your JDK path
        MAVEN_HOME = "C:\\Program Files\\Apache\\maven-3.9.0" // adjust if needed
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/yourusername/railway-reservation-system.git'
            }
        }

        stage('Build') {
            steps {
                bat "${MAVEN_HOME}\\bin\\mvn clean package"
            }
        }

        stage('Stop Existing App') {
            steps {
                // Kill process using port 8085 (change port if needed)
                bat "netstat -ano | findstr :8085"
                bat "for /f \"tokens=5\" %a in ('netstat -ano ^| findstr :8085') do taskkill /PID %a /F"
            }
        }

        stage('Deploy') {
            steps {
                bat "java -jar target\\railway-reservation-1.0.0.jar"
            }
        }
    }

    post {
        failure {
            echo 'Build or deployment failed!'
        }
        success {
            echo 'Build and deployment successful!'
        }
    }
}
