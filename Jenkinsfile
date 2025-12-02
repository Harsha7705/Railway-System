pipeline {
    agent any

    tools {
        maven 'Maven3'    // Make sure Jenkins has this tool configured
        jdk   'Java21'        // Or whatever version your project uses
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean install -DskipTests=false'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
