pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKERHUB_CREDENTIALS_ID = '6ac063cd-f3fe-4461-93f1-ddcb7e31c487' 
        IMAGE_NAME = 'jsahayad/swe645project2'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh '/usr/bin/docker build -t jsahayad/swe645project2:latest .'
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
