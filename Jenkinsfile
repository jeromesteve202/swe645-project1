pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKERHUB_CREDENTIALS_ID = 'DOCKERHUB_CREDENTIALS_ID' 
        IMAGE_NAME = 'jsahayad/swe645project2'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME:latest .'
                }
            }
        }
        stage('Publish') {
            steps {
                script {
                    sh 'echo $DOCKERHUB_PASS | docker login $DOCKER_REGISTRY --username $DOCKERHUB_USER --password-stdin'
                    sh 'docker push $IMAGE_NAME:latest'
                }
            }
        }
    }
}
