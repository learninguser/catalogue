pipeline {
    agent {
        node {
            label 'agent-1'
        }
    }
    environment{
        packageVersion = ''
    }
    options {
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Pick something')
    }
    // Build stage
    stages {
        stage('Get the version'){
            steps {
                script {
                    def packageJSON = readJSON file: "package.json"
                    packageVersion = packageJSON.version
                    echo "Application verison: ${packageVersion}"
                }
            }
        }
        stage('Install dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
        stage('Deploy'){
            steps {
                echo "Hello ${params.action}"
            }
        }
    }
    // post build
    post {
        always {
            echo "I will always run"
        }
        success {
            echo "Runs only if pipeline is succeded"
        }
        failure {
            echo "Runs only if pipeline is failed"
        }
        changed {
            echo "Runs only if there is change in state compared to previous"
        }
    }
}