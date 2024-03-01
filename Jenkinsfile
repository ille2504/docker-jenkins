def gv

pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
    }
    parameters {
        choice(name: 'VERSION', choices: ['1.0.0', '1.0.2'], description: '')
    }
    environment {
        NEW_VERSION = '1.0.0'
    }
    stages {
        stage('init') {
            steps {
                script {
                    gv.sayHello()
                }
            }
        }
        stage('Build') {
            steps {
                echo "Building.."
                echo "The new version: ${NEW_VERSION}"
                sh '''
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                python3 hello.py
                python3 hello.py --name=Mario
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
    post {
        always {
            echo 'FINISH'
        }
        success {
            echo 'SUCCESS'
        }
        failure {
            echo 'FAILURE'
        }
    }
}