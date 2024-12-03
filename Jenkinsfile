pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/rjteche/apachewebsite.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def app = docker.build("rjteche/apachewebsite:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        app.push("latest")
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8080:80 rjteche/apachewebsite:latest'
            }
        }
    }
}
