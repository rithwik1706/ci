pipeline {
    agent any

    environment {
        PM2_HOME = "C:\\Users\\LAXMAN SAI\\.pm2"
        PATH = "C:\\Program Files\\nodejs;C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm;${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "📦 Checking out latest code..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "📦 Installing dependencies..."
                bat 'npm install'
            }
        }

        stage('Restart App with PM2') {
            steps {
                echo "🚀 Restarting app with PM2..."
                bat '''
                    echo Checking PM2 path:
                    where pm2
                    
                    echo Deleting old process (if exists)...
                    pm2 delete express-hi 1>nul 2>&1 || echo "No existing process"

                    echo Starting new process...
                    pm2 start index.js --name "express-hi"

                    echo Saving PM2 process list...
                    pm2 save

                    echo ✅ App restarted successfully!
                '''
            }
        }

        stage('Post-Deployment Check') {
            steps {
                echo "🔍 Checking if app is running..."
                bat '''
                    pm2 list
                    pm2 show express-hi
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed — check Jenkins console output."
        }
    }
}
