pipeline {
    agent any

    stages {
        stage('Setup parameters') {
            steps {
                script {
                    properties([
                                parameters([
                                [$class: 'ChoiceParameter',
                                    choiceType: 'PT_SINGLE_SELECT',
                                    description: 'Select the Environemnt from the Dropdown List',
                                    filterLength: 1,
                                    filterable: false,
                                    name: 'ENVIRONMENT',
                                    script: [
                                        $class: 'GroovyScript',
                                        fallbackScript: [
                                            classpath: [],
                                            sandbox: false,
                                            script:
                                                "return['Could not get The environemnts']"
                                        ],
                                        script: [
                                            classpath: [],
                                            sandbox: false,
                                            script:
                                                "return['Proceed','Abort']"
                                        ]
                                    ]
                                ],
                    ])
                    ])
                }
            }
        }
            stage('Cloning our Git') {
                when {
                expression {
                    return params.ENVIRONMENT == 'Proceed'
                }
                }
                steps {
                    git 'https://github.com/somu1679/dockertest1.git'
                }
            }
            stage('Copy the Index FIles to Nginx Html Folder') {
                when {
                expression {
                    return params.ENVIRONMENT == 'Proceed'
                }
                }
                steps {
                    sh 'sudo cp /var/lib/jenkins/workspace/sample-pipeline/*.* /var/www/html/'
                }
            }
            stage('Restart the NGINX Sever') {
                when {
                expression {
                    return params.ENVIRONMENT == 'Proceed'
                }
                }
                steps {
                    sh 'sudo systemctl restart nginx'
                    sh 'sudo systemctl status nginx'
                }
            }
            stage('Verifying The Deployment') {
                when {
                expression {
                    return params.ENVIRONMENT == 'Proceed'
                }
                }
                steps {
                    sh 'ls /var/www/html/'
                }
            }
    }
}
