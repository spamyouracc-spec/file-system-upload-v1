pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'spamyouracc-spec/file-system-upload-v1'
        DOCKER_TAG = 'v1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/spamyouracc-spec/file-system-upload-v1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'node -v'
                bat 'npm install'
            }
        }

        stage('Build App') {
            steps {
                bat 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:%DOCKER_TAG% .'
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat '''
                        docker login -u %DOCKER_USER% --password-stdin <<< %DOCKER_PASS%
                        docker push %DOCKER_IMAGE%:%DOCKER_TAG%
                    '''
                }
            }
        }
    }
}
