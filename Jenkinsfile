pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                git branch: 'main', url: 'https://github.com/rithwik1706/ci.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Restart App with PM2') {
            steps {
                // Stop if running, then start fresh
                bat '''
                pm2 stop express-hi || echo "App not running"
                pm2 delete express-hi || echo "No process to delete"
                pm2 start app.js --name express-hi
                pm2 save
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful — App is running under PM2!'
        }
        failure {
            echo '❌ Deployment failed — Check Jenkins logs.'
        }
    }
}
