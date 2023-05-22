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
        deploy('dev', 'greetings-app-dev', 7001)
        test('dev', 'greetings_dev')

        deploy('staging', 'greetings-app-staging', 7002)
        test('staging', 'greetings_staging')

        deploy('preprod', 'greetings-app-preprod', 7003)
        test('preprod', 'greetings_preprod')

        deploy('prod', 'greetings-app-prod', 7004)
        test('prod', 'greetings_prod')
    }
}


def deploy(String stageName, String appName, int port) {
    stage("deploy-to-${stageName}") {
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
}

def test(String stageName, String testCommand) {
    stage("tests-on-${stageName}") {
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
}
