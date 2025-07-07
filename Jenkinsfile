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

                    RUN pip install --no-cache-dir flask

                    EXPOSE 5000

                    CMD ["python", "app.py"]
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myimage'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d --name firstcontainer -p 5000:5000 myimage'
            }
        }
    }
}
