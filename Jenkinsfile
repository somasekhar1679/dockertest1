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
                                    name: 'CONFIRMATION',
                                    randomName: 'choice-parameter-57174574518627',
                                    script: [
                                        $class: 'GroovyScript',
                                        fallbackScript: [
                                            classpath: [],
                                            sandbox: false,
                                            script:
                                                   ''
                                        ],
                                        script: [
                                            classpath: [],
                                            sandbox: false,
                                            script:
                                                'return ["Proceed", "Abort"]'
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
                    return params.CONFIRMATION == 'Proceed'
                }
                }
                steps {
                    git 'https://github.com/somu1679/dockertest1.git'
                }
            }
            stage('Copy the Index FIles to Nginx Html Folder') {
                when {
                expression {
                    return params.CONFIRMATION == 'Proceed'
                }
                }
                steps {
                    sh 'sudo cp /var/lib/jenkins/workspace/sample-pipeline/*.* /var/www/html/'
                }
            }
            stage('Restart the NGINX Sever') {
                when {
                expression {
                    return params.CONFIRMATION == 'Proceed'
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
                    return params.CONFIRMATION == 'Proceed'
                }
                }
                steps {
                    sh 'ls /var/www/html/'
                }
            }
    }
}
