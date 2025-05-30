pipeline {
    agent any

    environment {
        IMAGE_NAME = "yourdockerhubusername/website"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/hshar/website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME:$BRANCH_NAME .'
                }
            }
        }

        stage('Publish If Master') {
            when {
                branch 'master'
            }
            steps {
                script {
                    sh 'docker rm -f website || true'
                    sh 'docker run -d -p 82:80 --name website $IMAGE_NAME:master'
                }
            }
        }
    }
}

