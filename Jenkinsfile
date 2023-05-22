pipeline {
    agent any

    
    stages {
        stage('Remove Existing Directory') {
            steps {
                bat 'rmdir /S /Q python-greetings'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
            }
        }
        stage('install-pip-deps') {
            steps {
                echo 'Installing all required dependencies...'
                bat 'dir'
                bat 'pip --version'
                bat 'pip install -r flask==2.3.2'
            }
        }
        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                bat 'pm2 delete greetings-app-dev || true'
                bat 'pm2 start app.py --name greetings-app-dev -- --port 7001'
            }
        }
        stage('tests-on-dev') {
            steps {
                echo 'Running tests on dev...'
                bat 'npm install'
                bat 'npm run greetings greetings_dev'
            }
        }
        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging...'
                bat 'pm2 delete greetings-app-staging || true'
                bat 'pm2 start app.py --name greetings-app-staging -- --port 7002'
            }
        }
        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging...'
                bat 'npm install'
                bat 'npm run greetings greetings_staging'
            }
        }
        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to preprod...'
                bat 'pm2 delete greetings-app-preprod || true'
                bat 'pm2 start app.py --name greetings-app-preprod -- --port 7003'
            }
        }
        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on preprod...'
                bat 'npm install'
                bat 'npm run greetings greetings_preprod'
            }
        }
        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to prod...'
                bat 'pm2 delete greetings-app-prod || true'
                bat 'pm2 start app.py --name greetings-app-prod -- --port 7004'
            }
        }
        stage('tests-on-prod') {
            steps {
                echo 'Running tests on prod...'
                bat 'npm install'
                bat 'npm run greetings greetings_prod'
            }
        }
    }
}
