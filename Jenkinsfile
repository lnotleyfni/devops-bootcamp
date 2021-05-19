pipeline {
    agent any
    tools {
        nodejs 'lnotley-nodejs-installation'
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'npm install'
            }
        }
    }
}