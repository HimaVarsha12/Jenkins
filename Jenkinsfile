pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/user/repository.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package' // Java Example
                // For Node.js: sh 'npm install'
                // For Python: sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test' // Run unit tests
            }
        }

        stage('Deploy to Staging') {
            steps {
                sh './deploy.sh staging' // Custom deployment script
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                sh './deploy.sh production'
            }
        }
    }
}
