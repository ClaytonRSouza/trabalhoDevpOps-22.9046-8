pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/SeuUsuario/Trabalho_DevOps_RA.git'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pip install -r app/requirements.txt'
                sh 'python -m unittest discover tests'
            }
        }
        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Deploy Containers') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
    }
}
