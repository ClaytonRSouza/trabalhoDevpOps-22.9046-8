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
                    sh 'docker-compose build'  // Certifique-se de usar o comando correto com `docker-compose`

                    // Subir os containers do Docker com Docker Compose
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Rodar Testes') {
            steps {
                script {
                    // Aguardar que os containers estejam prontos
                    sh 'sleep 40'  // Ajuste o tempo de espera conforme necessário, mas prefira uma verificação mais confiável

                    // Verificar se o serviço de testes está disponível antes de rodar os testes
                    sh '''
                        docker-compose exec flask curl --fail http://localhost:5000 || exit 1
                    '''  // Adapte o comando conforme o seu serviço (a URL pode ser diferente)

                    // Rodar os testes no container adequado
                    sh 'docker-compose run --rm flask pytest /flask/test_app.py'  // Ajuste o caminho para o arquivo de teste
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
