pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('my-app')
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('my-app').inside {
                        sh 'npm test'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.image('my-app').push('my-app:latest')
                    sh 'kubectl apply -f k8s/deployment.yaml'
                }
            }
        }
    }
}