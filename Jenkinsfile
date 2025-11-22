pipeline {
    agent any
stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Aakashnadarr/devops.git', branch: 'master'
            }
        }
    stages {

        stage('Install Nginx') {
            steps {
                sh '''
                    sudo apt-get update -y
                    sudo apt-get install nginx -y
                    sudo systemctl enable nginx
                    sudo systemctl start nginx
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

        stage('Restart Nginx') {
            steps {
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
