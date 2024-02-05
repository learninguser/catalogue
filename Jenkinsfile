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
        stage('Build'){
            steps {
                sh """
                    zip -q -r catalogue.zip ./* -x ".git" -x "*.zip" -x "Jenkinsfile"
                """
            }
        }
    }
    // post build
    post {
        always {
            deleteDir()
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