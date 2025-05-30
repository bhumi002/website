pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo "Cloning branch: ${env.BRANCH_NAME}"
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/bhumi002/website.git'
            }
        }

        stage('Build') {
            steps {
                echo "Running build step"
                // Add actual build commands here
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo "Deploying to port 80 (only on master branch)"
                sh '''
                    sudo docker build -t my-app .
                    sudo docker stop my-app || true
                    sudo docker rm my-app || true
                    sudo docker run -d -p 80:80 --name my-app my-app
                '''
            }
        }
    }
}
