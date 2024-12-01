# Documentação do projeto

Autor: Clayton Robert da Silva Souza
RA: 229046-8

## Descrição
Este repositório contém um projeto de DevOps que visa configurar um ambiente de monitoramento com Prometheus, Grafana, MySQL/MariaDB e Flask. O objetivo do projeto é fornecer métricas de desempenho em tempo real, utilizando Grafana para exibição de dashboards interativos.

## Estrutura do Projeto
A estrutura do repositório é a seguinte:

Copiar código
.
├── Jenkinsfile                   # Arquivo para o pipeline de CI/CD no Jenkins
├── README.md                     # Documentação do projeto
├── docker-compose.yml            # Arquivo para configuração dos containers Docker
├── estrutura.txt                 # Detalhes sobre a estrutura do projeto
├── exporter
│   └── mysqld_exporter.env       # Arquivo de configuração para o MySQL Exporter
├── flask
│   ├── Dockerfile_flask          # Dockerfile para o container do Flask
│   ├── app.py                    # Código principal da aplicação Flask
│   ├── requirements.txt          # Dependências do Flask
│   └── test_flask_app.py         # Arquivo de teste para o Flask
├── grafana
│   ├── Dockerfile_grafana        # Dockerfile para o container do Grafana
│   ├── dashboards
│   │   └── mariadb_dashboard.json # Dashboard para visualização das métricas
│   └── provisioning
│       ├── dashboard.yml         # Configuração de provisionamento do dashboard
│       └── datasource.yml        # Configuração de provisionamento da fonte de dados
├── mariadb
│   └── Dockerfile_mariadb        # Dockerfile para o container do MariaDB
└── prometheus
    └── prometheus.yml            # Arquivo de configuração do Prometheus

## Dependências
Este projeto utiliza as seguintes tecnologias e ferramentas:

Docker: Para a criação e gerenciamento de containers.
Docker Compose: Para facilitar a orquestração dos containers.
Flask: Framework web para Python utilizado para criar a API que interage com o banco de dados MariaDB.
MariaDB: Banco de dados relacional utilizado para armazenar os dados.
Prometheus: Sistema de monitoramento e coleta de métricas.
Grafana: Plataforma de visualização de dados, configurada para exibir as métricas coletadas pelo Prometheus.
Jenkins: Para automação do pipeline de integração contínua e deploy.
pytest: Framework de testes para garantir a integridade da aplicação.

## Configuração
Pré-requisitos
Instalar o Docker: Se você não tiver o Docker instalado, siga o guia oficial: Instalar o Docker
Instalar o Docker Compose: Caso também não tenha o Docker Compose instalado, siga este guia: Instalar o Docker Compose

## Passo a Passo para Rodar o Ambiente

### Clone o repositório:

Copiar código
git clone https://github.com/ClaytonRSouza/trabalhoDevpOps-22.9046-8.git
cd trabalhoDevpOps-22.9046-8
### Construa os containers com o Docker Compose:

Copiar código  
docker-compose up --build  
Esse comando irá construir as imagens necessárias e levantar os containers para o Flask, MariaDB, Prometheus, Grafana e MySQL Exporter.  

### Acesse a aplicação web:

Flask (API): Está disponível em http://localhost:5000/.  
Grafana: Está disponível em http://localhost:3000/. O login padrão é:  
Usuário: admin  
Senha: admin  
Prometheus: Está disponível em http://localhost:9090/.  

### Acessando os Dashboards no Grafana:

Após o Docker Compose concluir a configuração, a dashboard configurada será acessível no Grafana.  
Você deve ver o dashboard de MariaDB ou Prometheus.  

## Jenkins (CI/CD Pipeline)
Acesse o Jenkins em http://localhost:8080/.
Faça login com as credenciais configuradas.
Pipeline de CI/CD:
O Jenkinsfile está configurado para clonar o repositório, construir as imagens e realizar os testes com pytest.

## Instruções de Uso
### Flask API:

GET /alunos: Lista todos os alunos registrados no banco de dados.
POST /alunos: Adiciona um novo aluno no banco de dados (dados esperados no corpo da requisição como JSON).

### Grafana:

O Grafana irá coletar métricas do Prometheus e exibir gráficos com dados em tempo real sobre a aplicação Flask e o banco MariaDB.
O painel do Grafana foi configurado para monitorar as métricas de requisições HTTP, latência, e status das requisições.

### Prometheus:

O Prometheus coleta métricas do mysqld_exporter, que monitora o banco MariaDB.
