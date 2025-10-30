pipeline {
    agent any

    environment {
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
                echo '📥 Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Restart App with PM2') {
            steps {
                echo '🚀 Restarting app with PM2...'
                bat '''
                set PM2_HOME=C:\\Users\\LAXMAN SAI\\.pm2
                set PATH=C:\\Program Files\\nodejs;C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm;%PATH%

                echo Checking PM2 path:
                where pm2

                echo Deleting old process (if exists)...
                pm2 delete express-hi >nul 2>&1 || echo "No existing process"

                echo Starting app...
                pm2 start index.js --name express-hi || echo "PM2 start failed"

                echo Saving PM2 process list...
                pm2 save || echo "PM2 save skipped"

                echo Showing PM2 list:
                pm2 list
                '''
            }
        }

        stage('Post-Deployment Check') {
            steps {
                echo '🔍 Verifying PM2 status...'
                bat 'pm2 show express-hi || echo "PM2 show failed"'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful — app should be running on port 3000!'
        }
        failure {
            echo '⚠️ Deployment failed — check Jenkins console output.'
        }
    }
}
