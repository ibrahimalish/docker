pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build("flask-app")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    app.run("-d -p 5000:5000 --name my-flask-container")
                }
            }
        }
    }
}

