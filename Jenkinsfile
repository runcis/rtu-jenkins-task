pipeline {
    agent any
    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Installing all required dependencies...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'dir'
                bat 'pip3 install -r requirements.txt'
            }
        }
        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'pm2 delete greetings-app-dev || true'
                bat 'pm2 start app.py --name greetings-app-dev -- --port 7001'
            }
        }
        stage('tests-on-dev') {
            steps {
                echo 'Running tests on dev...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'npm install'
                bat 'npm run greetings greetings_dev'
            }
        }
        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'pm2 delete greetings-app-staging || true'
                bat 'pm2 start app.py --name greetings-app-staging -- --port 7002'
            }
        }
        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'npm install'
                bat 'npm run greetings greetings_staging'
            }
        }
        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to preprod...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'pm2 delete greetings-app-preprod || true'
                bat 'pm2 start app.py --name greetings-app-preprod -- --port 7003'
            }
        }
        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on preprod...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'npm install'
                bat 'npm run greetings greetings_preprod'
            }
        }
        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to prod...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'pm2 delete greetings-app-prod || true'
                bat 'pm2 start app.py --name greetings-app-prod -- --port 7004'
            }
        }
        stage('tests-on-prod') {
            steps {
                echo 'Running tests on prod...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'npm install'
                bat 'npm run greetings greetings_prod'
            }
        }
    }
}
