pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build("ibrahimalish/first:latest")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker rm -f my-flask-app'
                    app.run("-d -p 5000:5000 --name my-flask-app")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'docker login -u $USER -p $PASS'
                }


                    sh 'docker push ibrahimalish/first:latest'
                }
            }
        }
    }
}
