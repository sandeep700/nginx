pipeline {
    agent any
    }
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    docker.build("sandy700/nginx:latest:${TAG}")
                }
            }
        }
	    stage('Pushing Docker Image to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'sandy700') {
                        docker.image("sandy700/nginx:latest:${TAG}").push()
                        docker.image("sandy700/nginx:latest:${TAG}").push("latest")
                    }
                }
            }
        }
    }
