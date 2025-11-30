pipeline {
    agent any

    tools {
        jdk 'Java21'       // Your configured Java
        maven 'Maven3'     // Optional, can be left if not building
        git 'GitDefault'   // Optional, if you want Jenkins to use your Git tool
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Harsha7705/Railway-System.git'
            }
        }

        stage('Run JAR') {
            steps {
                // Use double quotes and call to handle Windows path
                bat 'java -jar "target/railway-reservation-1.0.0.jar"'
            }
        }
    }

    post {
        success {
            echo 'Application ran successfully!'
        }
        failure {
            echo 'Failed to run the application!'
        }
    }
}
