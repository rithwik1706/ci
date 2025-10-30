pipeline {
    agent any

    environment {
        // ✅ Define your actual PM2 home and PATH (important for Windows)
        PM2_HOME = "C:\\Users\\LAXMAN SAI\\.pm2"
        PATH = "C:\\Program Files\\nodejs;C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm;${PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo '📦 Checking out latest code...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '📥 Installing npm packages...'
                bat 'npm install'
            }
        }

        stage('Restart App with PM2') {
            steps {
                echo '🚀 Restarting app using PM2...'
                bat '''
                set PM2_HOME=C:\\Users\\LAXMAN SAI\\.pm2
                set PATH=C:\\Program Files\\nodejs;C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm;%PATH%
                
                echo Current PM2 location:
                where pm2

                echo Deleting old process if exists...
                pm2 delete express-hi || echo "No previous process"

                echo Starting new app process...
                pm2 start index.js --name express-hi

                echo Saving PM2 process list...
                pm2 save

                echo Final PM2 status:
                pm2 list
                '''
            }
        }

        stage('Post-Deployment Check') {
            steps {
                echo '🔍 Checking if app started successfully...'
                bat 'pm2 show express-hi'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful — App is running under PM2!'
        }
        failure {
            echo '❌ Deployment failed — Check Jenkins logs for details.'
        }
    }
}
