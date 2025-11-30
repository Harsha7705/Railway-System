pipeline {
    agent any

    tools {
        maven 'Maven3' // match the name you gave in Jenkins
        jdk 'Java21'   // make sure Java is configured in Jenkins too
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Harsha7705/Railway-System.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Run') {
            steps {
                bat 'java -jar target/railway-reservation-system-0.0.1-SNAPSHOT.jar'
            }
        }
    }

    post {
        success { echo 'Build and tests successful!' }
        failure { echo 'Build or tests failed!' }
    }
}
