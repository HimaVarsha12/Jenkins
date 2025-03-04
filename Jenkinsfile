pipeline {
    agent any  // Runs on any available Windows agent

    environment {
        NODEJS_HOME = "C:\\Program Files\\nodejs"  // Modify based on actual Node.js installation path
        PATH = "${NODEJS_HOME};${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    echo "Cloning repository..."
                    checkout([$class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[url: 'https://github.com/HimaVarsha12/Jenkins/']]
                    ])
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    echo "Installing dependencies..."
                    bat 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    echo "Running Selenium tests..."
                    bat 'npm test'
                }
            }
        }

        stage('Build Application') {
            steps {
                script {
                    echo "Building application..."
                    bat 'npm run build'  // Modify if using a different build command
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo "Deploying to Staging Environment..."
                    bat 'scp -r ./dist user@staging-server:C:/staging-app/'  // Modify for your staging setup
                    bat 'ssh user@staging-server "C:/staging-app/restart-server.bat"' // Restart staging server
                }
            }
        }

        stage('Approval for Production') {
            steps {
                input message: 'Approve deployment to Production?', ok: 'Deploy'
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo "Deploying to Production Environment..."
                    bat 'scp -r ./dist user@production-server:C:/production-app/'  // Modify for your production setup
                    bat 'ssh user@production-server "C:/production-app/restart-server.bat"' // Restart production server
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline execution failed!"
        }
    }
}
