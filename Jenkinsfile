pipeline {
    agent any
    parameters {
        string(name: 'GREETING', defaultValue: 'Hello', description: 'The greeting message')
        choice(name: 'BRANCH', choices: ['master', 'dev'], description: 'Branch to build')
    }
    stages {
        stage('Example') {
            steps {
                echo "${params.GREETING}, we are building the ${params.BRANCH} branch."
            }
        }
    }
}
