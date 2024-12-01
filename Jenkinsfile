pipeline {
    agent any

    environment {
        REPOSITORY_URL = 'https://github.com/ClaytonRSouza/trabalhoDevpOps-22.9046-8.git'
        BRANCH_NAME = 'main'
        GIT_CREDENTIALS_ID = 'github-https-credentials'  // ID da credencial do tipo "Username with password"
    }

    stages {
        stage('Baixar código do Git') {
            steps {
                // Clonar o repositório do Git utilizando HTTPS e credenciais do Jenkins
                git credentialsId: "${GIT_CREDENTIALS_ID}", branch: "${BRANCH_NAME}", url: "${REPOSITORY_URL}"
            }
        }

        stage('Build e Deploy') {
            steps {
                script {
                    // Construir as imagens Docker para cada serviço
                    sh '''
                        docker compose build
                    '''

                    // Subir os containers do Docker com Docker Compose
                    sh '''
                        docker compose up -d
                    '''
                }
            }
        }

        stage('Rodar Testes') {
            steps {
                script {
                    // Rodar os testes com o pytest ou qualquer outra ferramenta de testes
                    sh 'sleep 40'  // Ajuste o tempo de espera conforme necessário
                    sh 'docker compose run --rm test'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executada com sucesso!'
        }
        failure {
            echo 'A pipeline falhou.'
        }
    }
}
