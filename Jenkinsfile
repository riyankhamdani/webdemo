pipeline {
    agent any
      
      stages{
        stage('Install NGINX') {
            steps {
                echo 'Installing Nginx ...'
                sh '''
                   sudo yum install nginx -y
                   sudo systemctl enable nginx
                   sudo systemctl start nginx
                '''
            }
        }

        stage('Check NGINX status') {
            steps {
                echo 'Checking Nginx service status...'
                sh 'sudo systemctl status nginx'
                echo 'Checking Nginx HTTP response...'
                sh 'sudo curl -I http://localhost'
            }
        }	

        stage('Set Firewall for NGINX') {
            steps {
                echo 'Setting firewall for NGINX...'
                sh 'sudo firewall-cmd --permanent --add-service=http'
                sh 'sudo firewall-cmd --reload'
                sh 'sudo firewall-cmd --list-all | grep services'
                echo 'Setting firewall is done...'
            }
        }

        stage('Change Home Page') {
            steps {
                echo 'Changing the Home Page...'
                sh 'sudo cp /var/lib/jenkins/workspace/pipeline-demo1/github/index.html /usr/share/nginx/html/index.html'
                sh 'cat /usr/share/nginx/html/index.html'
                echo 'Changing the Home Page...'
            }
        }

        stage('Test The Home Page') {
            steps {
                echo 'Test the Home Page...'
                sh 'curl http://devopsdemo.com'
                echo 'The Change of Home Page is Successfully Tested...'
            }
        }
    }
}    