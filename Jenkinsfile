pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Vikashguliya/flask-ci-cd.git',
                    credentialsId: 'github-token'
            }
        }

        stage('Build') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -c "import flask; print(\'Flask OK\')"'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop flask-app || true
                docker rm flask-app || true
                docker build -t flask-app .
                docker run -d -p 5000:5000 --name flask-app flask-app
                '''
            }
        }
    }
}
