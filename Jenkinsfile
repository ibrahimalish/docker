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
                    sh '''
                    if [ "$(docker ps -aq -f name=my-flask-app)" ]; then
                        docker stop my-flask-app || true
                        docker rm my-flask-app || true
                    fi
                    '''
                    app.run("-d -p 5000:5000 --name my-flask-app")
                }
            }
        }
    }
}

