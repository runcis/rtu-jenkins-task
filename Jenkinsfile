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
                dir('python-greetings') {
                    bat '''
                        python -m pip --version
                        python -m pip install -r requirements.txt
                    '''
                }
            }
        }
        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                dir('python-greetings') {
                    bat '''
                        "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" --version
                        "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-dev -- --port 7001
                    '''
                }
            }
        }
        stage('tests-on-dev') {
            steps {
                echo 'Running tests on dev...'
                
                bat 'git clone https://github.com/mtararujs/course-js-api-framework.git'
                dir('course-js-api-framework') {
                    bat '''
                        npm install
                        npm run greetings greetings_dev
                    '''
                }
            }
        }
        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging...'
                dir('python-greetings') {
                    bat '''
                        "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete greetings-app-staging & set "errorlevel=0"
                        "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-staging -- --port 7002
                    '''
                }
            }
        }
        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging...'

                bat 'git clone https://github.com/mtararujs/course-js-api-framework.git'
                dir('course-js-api-framework') {
                    bat '''
                        npm install
                        npm run greetings greetings_staging
                    '''
                }
            }
        }
        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to preprod...'
                
                dir('python-greetings') {
                    bat '''
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete greetings-app-preprod & set "errorlevel=0"
                    "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-preprod -- --port 7003
                    '''
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on preprod...'
                bat 'git clone https://github.com/mtararujs/course-js-api-framework.git'
                dir('course-js-api-framework') {
                    bat '''
                        npm install
                        npm run greetings greetings_preprod
                    '''
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to prod...'
                
                dir('python-greetings') {
                    bat '''
                        "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete greetings-app-prod & set "errorlevel=0"
                        "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name greetings-app-prod -- --port 7004
                    '''
                }
            }
        }
        stage('tests-on-prod') {
            steps {
                echo 'Running tests on prod...'
                bat 'git clone https://github.com/mtararujs/course-js-api-framework.git'
                dir('course-js-api-framework') {
                    bat '''
                        npm install
                        npm run greetings greetings_prod
                    '''
                }
            }
        }
    }
}
