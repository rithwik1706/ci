pipeline {
    agent any

    environment {
        // PM2 and Node paths for Windows
        PM2_HOME = "C:\\Users\\LAXMAN SAI\\.pm2"
        PATH = "C:\\Program Files\\nodejs;C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm;${PATH}"
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
                echo 'Installing dependencies...'
                bat 'npm install'
            }
        }

        stage('Deploy with PM2') {
            steps {
                echo 'Restarting app with PM2...'
                bat '''
                "C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm\\pm2.cmd" delete express-hi || exit 0
                "C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm\\pm2.cmd" start app.js --name express-hi
                "C:\\Users\\LAXMAN SAI\\AppData\\Roaming\\npm\\pm2.cmd" save
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful!'
        }
        failure {
            echo '❌ Build or deployment failed.'
        }
    }
}
