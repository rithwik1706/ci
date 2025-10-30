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
                pm2 start app.js --name express-hi
                pm2 save
                '''
            }
        }
    }
}
