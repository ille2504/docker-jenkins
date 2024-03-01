def gv

pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
    }
       triggers {
        pollSCM '*/5 * * * *'
    }
    environment {
        NEW_VERSION = '1.0.0'
    }
    stages {
        stage('init') {
            steps {
                script {
                    gv = load "script.groovy"
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
                script {
                    gv.sayHello()
                }
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