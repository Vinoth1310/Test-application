pipeline {
    agent any 

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }

    stages {
        stage('SCM Checkout') {
            steps {
                sh 'rm -rf nodedemo || true'  // Remove existing directory if it exists
                sh 'git clone https://github.com/Vinoth1310/Test-application.git'
                echo 'test1'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'test2'
                sh 'docker build -t vinoth1310/sample-project:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        sh "docker login -u vinoth1310 -p Vinoth@1310"
                    }
                    echo 'test3'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push vinoth1310/sample-project:latest '
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
