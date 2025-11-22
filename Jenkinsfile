pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/AMIRMUJAWAR-WEB/nginix.git', branch: 'main'
            }
        }

        stage('Stop & Disable Nginx') {
            steps {
                sh '''
                    sudo systemctl stop nginx || true
                    sudo systemctl disable nginx || true
                '''
            }
        }

        stage('Install Apache') {
            steps {
                sh '''
                    sudo apt-get update -y
                    sudo apt-get install apache2 -y
                    sudo systemctl enable apache2
                    sudo systemctl start apache2
                '''
            }
        }

        stage('Deploy index.html') {
            steps {
                sh '''
                    sudo rm -f /var/www/html/index.html
                    sudo cp index.html /var/www/html/index.html
                    sudo chown www-data:www-data /var/www/html/index.html
                '''
            }
        }

        stage('Restart Apache') {
            steps {
                sh 'sudo systemctl restart apache2'
            }
        }
    }
}
