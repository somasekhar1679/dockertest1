pipeline {
    environment {

    }
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/mavrick202/dockertest1.git'
            }
        }
        stage('Copy the Index FIles to Nginx Html Folder') {
            steps {
                sh "cp /var/lib/jenkins/workspace/ECS_JENKINS/*.* /var/www/html/"
            }
        }
        stage('Restart the NGINX Sever') {
            steps {
                sh "systemctl restart nginx"
                sh "systemctl status nginx"
                
            }
        }
        stage('Verifying The Deployment') {
            steps {
                sh 'ls /var/www/html/'
                }
        }
    }
}
