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
            deploy('dev', 'greetings-app-dev', 7001)
        }
        stage('tests-on-dev') {
            test('dev', 'greetings_dev')
        }
        stage('deploy-to-staging') {
            deploy('staging', 'greetings-app-staging', 7002)
        }
        stage('tests-on-staging') {
            test('staging', 'greetings_staging')
        }
        stage('deploy-to-preprod') {
            deploy('preprod', 'greetings-app-preprod', 7003)
        }
        stage('tests-on-preprod') {
            test('preprod', 'greetings_preprod')
        }
        stage('deploy-to-prod') {
            deploy('prod', 'greetings-app-prod', 7004)
        }
        stage('tests-on-prod') {
            test('prod', 'greetings_prod')
        }
    }
}


def deploy(String stageName, String appName, int port) {
    steps {
        echo "Deploying to ${stageName}..."
        dir('python-greetings') {
            bat """
                "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" delete ${appName} & EXIT /B 0"
                "C:\\Users\\rinal\\AppData\\Roaming\\npm\\pm2" start app.py --name ${appName} -- --port ${port}
            """
        }
    }
}

def test(String stageName, String testCommand) {
    steps {
        echo "Running tests on ${stageName}..."
        dir('course-js-api-framework') {
            bat """
                npm install
                npm run greetings ${testCommand}
            """
        }
    }
}
