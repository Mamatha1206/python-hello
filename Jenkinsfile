pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git (url :'https://github.com/Mamatha1206/python-hello.git', branch:'main')
            }
        }

        stage('Set Up Python Environment') {
            steps {
                sh '''#!/bin/bash
                python3 -m venv ${VENV_DIR}
                . ${VENV_DIR}/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''#!/bin/bash
                . ${VENV_DIR}/bin/activate
                pytest
                '''
            }
        }

        stage('Run Hello World Script') {
            steps {
                sh '''#!/bin/bash
                . ${VENV_DIR}/bin/activate
                python hello.py
                '''
            }
        }

        stage('Build Artifacts') {
            steps {
                sh '''#!/bin/bash
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
