pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/chandanhegde7/flask-application.git' 
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                    # Check installed packages
                    pip list
                '''
            }
        }
        stage('Check Python Version') {
            steps {
                sh '''
                    . venv/bin/activate
                    python --version
                    which pytest
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest test_app/
                '''
            }
        }
        stage('Build Docker Image') {
            steps {
                sh '''
                    . venv/bin/activate
                    docker build -t flask-app .
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    . venv/bin/activate
                    docker run -d -p 5000:5000 flask-app
                '''
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
