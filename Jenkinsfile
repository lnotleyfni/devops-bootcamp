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
        stage('Create Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerRepoCreds', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''
                        echo ======================
                        echo $AWS_SECRET_ACCESS_KEY
                        echo $AWS_ACCESS_KEY_ID
                        echo ======================

                        wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        dpkg -i ./docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        apt-get update
                        apt-get install -y awscli
                        docker build -t workshopuser7:latest .
                        docker tag workshopuser7:latest workshopuser7:${BUILD_NUMBER}
                        docker tag workshopuser7:latest 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser7:latest
                        $(aws ecr get-login --region us-east-1 | sed 's/-e none//g')
                        docker push 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser7:latest
                    '''
                }
            }
        }
    }
}