pipeline {
    agent any
    stages {
        stage('Generate Dockerfile') {
            steps {
                script {
                    writeFile file: 'Dockerfile', text: '''
                FROM python:3.10-slim

                WORKDIR /app
                COPY . /app

                RUN pip install flask

                EXPOSE 5000

                CMD ["python", "app.py"]
                    '''
                }
            }
        }

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
