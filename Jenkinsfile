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
                 bat '''
                    python -m pip --version
                    cd python-greetings
                    python -m pip install -r requirements.txt
                '''
            }
        }
        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                bat '''
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" --version
                    cd python-greetings
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-dev -- --port 7001
                '''
            }
        }
        stage('tests-on-dev') {
            steps {
                echo 'Running tests on dev...'

                bat '''
                    npm install
                    npm run greetings greetings_dev
                '''
            }
        }
        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging...'

                bat '''
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete greetings-app-staging || true
                    cd python-greetings
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-staging -- --port 7002
                '''
            }
        }
        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging...'

                bat '''
                    npm install
                    npm run greetings greetings_staging
                '''
            }
        }
        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to preprod...'
                bat '''
                "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete greetings-app-preprod || true
                "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-preprod -- --port 7003
                '''
            }
        }
        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on preprod...'
                bat '''
                    npm install
                    npm run greetings greetings_preprod
                '''
            }
        }
        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to prod...'
                bat '''
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete greetings-app-prod || true
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-prod -- --port 7004
                '''
            }
        }
        stage('tests-on-prod') {
            steps {
                echo 'Running tests on prod...'
                
                bat '''
                    npm install
                    npm run greetings greetings_prod
                '''
            }
        }
    }
}
