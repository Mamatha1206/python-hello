pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git (url: 'https://github.com/Mamatha1206/python-hello.git',branch:'main')
            }
        }

        stage('Set Up Python Environment') {
            steps {
                sh '''
                python3 -m venv ${VENV_DIR}
                source ${VENV_DIR}/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source ${VENV_DIR}/bin/activate
                pytest
                '''
            }
        }

        stage('Build Artifacts') {
            steps {
                sh '''
                mkdir -p build
                cp hello.py build/
                '''
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }
}
