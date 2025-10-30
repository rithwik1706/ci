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
                bat '''
                pm2 stop express-hi || echo "App not running"
                pm2 delete express-hi || echo "No existing app"
                pm2 start index.js --name express-hi
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
