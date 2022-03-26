pipeline {
    agent any

    stages {
        stage ('Prompt for input') {
            steps {
                script {
                    env.USERNAME = input message: 'Please enter the username',
                             parameters: [string(defaultValue: '',
                                          description: '',
                                          name: 'Username')]
                    env.PASSWORD = input message: 'Please enter the password',
                             parameters: [password(defaultValue: '',
                                          description: '',
                                          name: 'Password')]
                }
                echo "Username: ${env.USERNAME}"
                echo "Password: ${env.PASSWORD}"
            }
        }
            stage('Cloning our Git') {
                steps {
                    git 'https://github.com/somu1679/dockertest1.git'
                }
            }
            stage('Copy the Index FIles to Nginx Html Folder') {
                steps {
                    sh 'sudo cp /var/lib/jenkins/workspace/sample-pipeline/*.* /var/www/html/'
                }
            }
            stage('Restart the NGINX Sever') {
                steps {
                    sh 'sudo systemctl restart nginx'
                    sh 'sudo systemctl status nginx'
                }
            }
            stage('Verifying The Deployment') {
                steps {
                    sh 'ls /var/www/html/'
                }
            }
    }
}
