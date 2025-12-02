pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'Java21'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                bat 'mvn clean install -DskipTests=false'
            }
        }
    }

    post {
        always {
            // Don't fail pipeline if no test results exist
            junit testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true
        }
    }
}
