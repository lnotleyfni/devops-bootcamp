pipeline {
    agent any
    tools {
        nodejs 'lnotley-nodejs-installation'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Build'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Build Testing'
                sh 'npm test'
            }
        }
    }
}