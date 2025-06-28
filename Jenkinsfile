pipeline {
    agent any

    environment {
        DOCKERHUB = credentials('dockerhub')
        IMAGE_NAME = "gantalalitha/python-app"
    }

    stages {
        stage('Clone GitHub Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Lalitha891/Python-app.git'

            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('DockerHub Login') {
            steps {
                script {
                    sh """
                    echo ${DOCKERHUB_PSW} | docker login -u ${DOCKERHUB_USR} --password-stdin
                    """
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    dockerImage.push("latest")
                }
            }
        }

        stage('Logout') {
            steps {
                sh 'docker logout'
            }
        }
    }
}
