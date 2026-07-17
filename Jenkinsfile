pipeline {
    agent any
    environment {
        container_name = "cicd_nestjs-container"
        image_name = "cicd_nestjs-image"
        DOCKER_IMAGE = "saaz/cicd_nestjs"
        email = "u2022274@gmail.com"
        port = "3000"
    }
    stages {
        stage('clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/MALIKABDULLAHAWAN/CICD-DOCKER-JENKIN.git'
            }
        }
        stage('build docker image') {
            steps {
                sh 'docker build -t $image_name .'
            }
        }
        stage('stop and remove docker container') {
            steps {
                sh 'docker stop $container_name || true'
                sh 'docker rm $container_name || true'
            }
        }
        stage('run docker container') {
            steps {
                sh 'docker run -d -p $port:3000 --name $container_name $image_name'
            }
        }
        stage('send email') {
            when { expression { false } }
            steps {
                mail to: "$email",
                    subject: "Build #${BUILD_NUMBER} - Deployment Successful",
                    body: """
                    Build Status: SUCCESS
                    
                    Docker Container: $container_name
                    Image: $image_name
                    Port: $port
                    
                    Application URL: http://13.204.46.89:3000
                    
                    Jenkins Build: ${BUILD_URL}
                    """,
                    mimeType: 'text/plain'
            }
        }
    }
}
