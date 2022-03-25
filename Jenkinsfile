pipeline {
    agent any

    stages {
        stage('Setup parameters') {
            steps {
                script {
                    properties([
                        parameters([
                            choice(
                                choices: ['Proceed', 'Abort'],
                                name: 'Ready to go?'
                            )
                        ])
                    ])
                }
            }
        }

            stage('Confirmation to start the project...!') {
            when {
                expression {
                    return params.choice == 'Proceed'
                }
            }
            steps {
                script {
                    skipRemainingStages = true

                    println "skipRemainingStages = ${skipRemainingStages}"
                }
            }
            }
            stage('Cloning our Git') {
                steps {
                    git 'https://github.com/mavrick202/dockertest1.git'
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
