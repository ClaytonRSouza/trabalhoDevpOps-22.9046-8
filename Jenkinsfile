pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "my-flask-app"
        DOCKER_TAG = "latest"
        REGISTRY = "my-docker-registry"
        DOCKER_CREDENTIALS_ID = "dockerhub-credentials"
        GIT_CREDENTIALS_ID = "github-ssh-credentials-id"  // Adicionando as credenciais do GitHub
    }

    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: 'github-ssh-credentials-id', url: 'git@github.com:ClaytonRSouza/trabalhoDevpOps-22.9046-8.git', branch: 'main'
            }
        }

        stage('Run Tests') {
            steps {
                // Executa os testes da aplicação
                script {
                    sh 'pytest tests/'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                // Constrói as imagens Docker para a aplicação Flask e para o MariaDB Exporter
                script {
                    sh "docker build -t ${REGISTRY}/${DOCKER_IMAGE}:${DOCKER_TAG} -f Dockerfile_flask_app ."
                    sh "docker build -t ${REGISTRY}/mariadb_exporter:${DOCKER_TAG} -f Dockerfile_mariadb_exporter ."
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                // Realiza o push das imagens Docker para o registro
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        sh "docker push ${REGISTRY}/${DOCKER_IMAGE}:${DOCKER_TAG}"
                        sh "docker push ${REGISTRY}/mariadb_exporter:${DOCKER_TAG}"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Realiza o deploy do ambiente utilizando Docker Compose
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Verify Monitoring') {
            steps {
                // Verifica se o Prometheus e o Grafana estão funcionando
                script {
                    sh 'curl -f http://localhost:9090' // Verifica o Prometheus
                    sh 'curl -f http://localhost:3000' // Verifica o Grafana
                }
            }
        }
    }

    post {
        always {
            // Limpa os containers e imagens Docker locais
            script {
                sh 'docker-compose down'
                sh 'docker system prune -f'
            }
        }
        success {
            // Notifica o sucesso da pipeline
            echo 'Pipeline executed successfully!'
        }
        failure {
            // Notifica o fracasso da pipeline
            echo 'Pipeline execution failed!'
        }
    }
}
