pipeline {
    agent {
        docker {
            image 'ubuntu:20.04'
            args '-u root'
        }
    }
    environment {
        APP_DIR = "/var/www/html"
    }
    stages {
        stage('Install Apache and Git') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y apache2 git
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mkdir -p ${APP_DIR}
                    cp -r * ${APP_DIR}/
                '''
            }
        }

        stage('Publish to Port 82') {
            when {
                branch 'master'
            }
            steps {
                sh '''
                    sed -i 's/80/82/g' /etc/apache2/ports.conf
                    sed -i 's/80/82/g' /etc/apache2/sites-enabled/000-default.conf
                    apachectl restart
                    echo "Website published at port 82"
                '''
            }
        }
    }
}
