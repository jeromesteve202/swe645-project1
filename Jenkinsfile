pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = 'docker.io'
        // Remove the DOCKERHUB_CREDENTIALS_ID from here as it will be used directly in the withCredentials step
        IMAGE_NAME = 'jsahayad/swe645project2'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh '/usr/bin/docker build -t $IMAGE_NAME:latest .'
                }
            }
        }
        stage('Publish') {
            steps {
                script {
                    // Use the withCredentials step to securely pass credentials
                    withCredentials([usernamePassword(credentialsId: '6ac063cd-f3fe-4461-93f1-ddcb7e31c487', passwordVariable: 'DOCKERHUB_PASS', usernameVariable: 'DOCKERHUB_USER')]) {
                        sh "echo $DOCKERHUB_PASS | docker login $DOCKER_REGISTRY --username $DOCKERHUB_USER --password-stdin"
                        sh "docker push $IMAGE_NAME:latest"
                    }
                }
            }
        }
        stage('Deploy to Rancher') {
            steps {
                script {
                    // Assuming you have kubectl and necessary access configured in your Jenkins environment
                    sh 'kubectl rollout restart deployment swe645project2'
                }
            }
        }
    }
}