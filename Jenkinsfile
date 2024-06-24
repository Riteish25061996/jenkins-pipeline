pipeline {
    agent {
        
        label "built-in"
    }

    stages {
        stage('Install httpd') {
            steps {
                script {
                    sh '''
                        # Install httpd package
                        sudo yum install -y httpd
                        
                        # Start and enable httpd service
                        sudo systemctl start httpd
                        sudo systemctl enable httpd
                    '''
                }
            }
        }

        stage('Copy index.html') {
            steps {
                script {
                    sh '''
                        # Create sample index.html
                        echo "<html><body><h1>Hello, Swaraj!</h1></body></html>" > index.html
                        
                        # Copy index.html to /var/www/html
                        sudo cp index.html /var/www/html/index.html
                    '''
                }
            }
        }

        stage('Set Permissions') {
            steps {
                script {
                    sh '''
                        # Set permissions to ensure the web server can serve the file
                        sudo chmod 644 /var/www/html/index.html
                        
                        # Ensure the web server has the right ownership
                        sudo chown apache:apache /var/www/html/index.html
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'httpd installation and setup completed successfully.'
        }
        failure {
            echo 'httpd installation and setup failed.'
        }
    }
}

