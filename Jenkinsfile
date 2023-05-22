pipeline {
    agent any

    
    stages {
        stage('Remove Existing Directory') {
            steps {
                bat 'rmdir /S /Q python-greetings'
                bat 'rmdir /S /Q course-js-api-framework'
            }
        }
        stage('install-pip-deps-to-delete') {
            steps {
                
                echo 'Installing all required dependencies...'
                bat 'git clone https://github.com/mtararujs/python-greetings.git'
                bat 'git clone https://github.com/mtararujs/course-js-api-framework.git'
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
                script{
                    deploy('dev', 'greetings-app-dev', 7001)
                }
            }
        }
        stage('tests-on-dev') {
            steps {
                script{
                    test('dev', 'greetings_dev')
                }
            }
        }
        stage('deploy-to-staging') {
            steps {
                script{
                    deploy('staging', 'greetings-app-staging', 7002)
                }
            }
        }
        stage('tests-on-staging') {
            steps {
                script{
                    test('staging', 'greetings_staging')
                }
            }
        }
        stage('deploy-to-preprod') {
            steps {
                script{
                    deploy('preprod', 'greetings-app-preprod', 7003)
                }
            }
        }
        stage('tests-on-preprod') {
            steps {
                script{
                    test('preprod', 'greetings_preprod')
                }
            }
        }
        stage('deploy-to-prod') {
            steps {
                script{
                    deploy('prod', 'greetings-app-prod', 7004)
                }
            }
        }
        stage('tests-on-prod') {
            steps {
                script{
                    test('prod', 'greetings_prod')
                }
            }
        }
    }
}

def deploy(String stageName, String appName, int port) {
    echo "Deploying to ${stageName}..."
    dir('python-greetings') {
        bat """
            "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete ${appName} & EXIT /B 0"
            "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name ${appName} -- --port ${port}
        """
    }
}

def test(String stageName, String testCommand) {
    echo "Running tests on ${stageName}..."
    dir('course-js-api-framework') {
        bat """
            npm install
            npm run greetings ${testCommand}
        """
    }
}
