pipeline {
    agent any

    environment {
        // Path to Spring Boot project inside repo
        APP_DIR = 'demo/demo'
    }

    stages {

        stage('Checkout') {
            steps {
                // Checkout code from GitHub
                git branch: 'main', url: 'https://github.com/NAMPALLY-PRANAY/demo_spring.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spring Boot Application...'
                dir("${APP_DIR}") {
                    sh './mvnw clean package -DskipTests'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                dir("${APP_DIR}") {
                    sh './mvnw test'
                }
            }
        }

        stage('Run Application') {
            steps {
                echo 'Starting Spring Boot Application...'
                dir("${APP_DIR}") {
                    // Run in background for demo
                    sh 'nohup ./mvnw spring-boot:run &'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
