 pipeline {
    agent any

    stages {

        stage('Verify') {
        def userInput = input(
            id: 'userInput', message: 'This is PRODUCTION!', parameters: [
            [$class: 'BooleanParameterDefinition', defaultValue: false, description: '', name: 'Please confirm you sure to proceed']
        ])
        
        if(!userInput) {
            error "Build wasn't confirmed"
        }
    }
    }
}
