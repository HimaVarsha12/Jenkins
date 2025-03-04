pipeline {
    agent any

    environment {
        NODE_VERSION = '18'  // Specify the Node.js version
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/HimaVarsha12/Jenkins.git'
            }
        }

        stage('Setup Node.js') {
            steps {
                script {
                    def nodeHome = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${nodeHome}/bin:${env.PATH}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'  
            }
        }

        stage('Test') {
            steps {
                sh 'npm run test'  
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'  
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check logs for more details.'
        }
    }
}
