pipeline {
    agent any

    environment {
        APP_NAME = 'railway-reservation'
        JAR_NAME = 'railway-reservation-1.0.0.jar'
        PORT = 8085
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                retry(3) {
                    git branch: 'main', url: 'https://github.com/yourusername/railway-reservation-system.git'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Stop Existing App') {
            steps {
                echo "Stopping any existing app on port ${PORT}..."
                // Kill process on the port
                sh """
                if lsof -i :${PORT} -t >/dev/null; then
                    kill -9 \$(lsof -i :${PORT} -t)
                else
                    echo "No process running on port ${PORT}"
                fi
                """
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh "nohup java -jar target/${JAR_NAME} > app.log 2>&1 &"
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
