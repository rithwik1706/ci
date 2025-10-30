pipeline {
    agent any

    environment {
        // Force Jenkins to use your PM2 installation
        PM2_HOME = "C:\\Users\\LAXMAN SAI\\.pm2"
        PATH = "C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm;${PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling latest code...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing NPM packages...'
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo 'Build complete. No custom build steps yet.'
            }
        }

        stage('Deploy with PM2') {
            steps {
                echo 'Starting/Restarting Express app with PM2...'
                bat '''
                pm2 delete express-hi || exit 0
                pm2 start app.js --name express-hi
                pm2 save
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build and deploy successful!'
        }
        failure {
            echo '❌ Build or deployment failed.'
        }
    }
}
