pipeline {
    agent any 

    environment {
        DOCKER_IMAGE = 'shrutiv05/new-dockerimg:latest' // Replace with your Docker Hub username and image name
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/shrutiverma05/Docker_demo.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-cred', url: '']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                sh 'docker stop my-container || true'  // Stop if already running
                sh 'docker rm my-container || true'    // Remove if already exists
                sh 'docker run -d -p 8082:80 --name my-container $DOCKER_IMAGE'
            }
        }
    }
}

