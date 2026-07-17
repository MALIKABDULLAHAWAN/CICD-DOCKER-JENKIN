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
            steps {
                mail to: "$email",
                    subject: "Jenkins Build Notification",
                    body: "The build has been completed successfully."
            }
        }
    }
}
