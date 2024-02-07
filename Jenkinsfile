pipeline {
    agent {
        node {
            label 'agent-1'
        }
    }
    environment{
        projectName = "roboshop"
        component = "catalogue"
        nexusURL = "172.31.35.84:8081"
        packageVersion = ''
    }
    options {
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Set to true if deployment ready')
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