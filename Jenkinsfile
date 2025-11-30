pipeline {
    agent any

    tools {
        maven 'Maven3' 
        jdk 'Java21'   
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Harsha7705/Railway-System.git'
            }
        }

        stage('Build') {
            steps {
                bat '"mvn" clean package'
            }
        }

        stage('Test') {
            steps {
                bat '"mvn" test'
            }
        }

        stage('Run') {
            steps {
                echo 'Running the application...'
                bat '"java" -jar "target\\railway-reservation-1.0.0.jar"'
            }
        }
    }

    post {
        success {
            echo 'Build and tests successful!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
