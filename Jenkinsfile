pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'hello-world-python:1.0' // Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ravikiranmasule/jenkins_docker_python_hello_world.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    if (fileExists('Dockerfile')) {
                        sh "docker build -t ${env.DOCKER_IMAGE} ."
                    } else {
                        error "Dockerfile not found in the workspace."
                    }
                }
            }
        }

        stage('Docker Run (Optional)') {
            steps {
                sh "docker run --rm ${env.DOCKER_IMAGE}"
            }
        }
    

    post {
        success {
            echo 'Python application Docker image built successfully.'
        }
        failure {
            echo 'Docker build or run failed.'
        }
    }
}

