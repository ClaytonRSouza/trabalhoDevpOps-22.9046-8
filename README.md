# Documentação do Projeto DevOps: Monitoramento com Flask, MariaDB, Prometheus, Grafana, e Jenkins  
  
Autor: Clayton Robert da Silva Souza  
RA: 229046-8  
  
## Descrição  

Este repositório contém o código e a configuração de um projeto de DevOps, que visa criar um ambiente de monitoramento de desempenho para uma aplicação web baseada em Flask. O projeto utiliza as ferramentas Docker, Docker Compose, MariaDB, Prometheus, Grafana e Jenkins para coletar, exibir e monitorar métricas de desempenho da aplicação, como latência de requisições e estado do banco de dados.  

O sistema tem como objetivo demonstrar a integração de ferramentas de DevOps para automação de CI/CD e visualização de métricas em tempo real.  
  
## Dependências  
Este projeto depende das seguintes tecnologias:  
  
Docker: Plataforma para criação, deploy e execução de containers.  
Docker Compose: Ferramenta para orquestrar múltiplos containers.  
Flask: Framework web em Python utilizado para construir a API.  
MariaDB: Banco de dados relacional utilizado para armazenar as informações da aplicação.  
Prometheus: Ferramenta de monitoramento para coletar métricas de sistemas e serviços.  
Grafana: Plataforma de visualização de dados utilizada para exibir as métricas coletadas pelo Prometheus.  
Jenkins: Ferramenta de automação para implementar o pipeline de CI/CD.  
pytest: Framework de testes para validar o comportamento da aplicação Flask.  
  
## Passo a Passo para Rodar o Ambiente  
### 1. Clone o Repositório  
Execute o comando abaixo para clonar o repositório para sua máquina local:  
  
git clone https://github.com/ClaytonRSouza/trabalhoDevpOps-22.9046-8.git  
cd trabalhoDevpOps-22.9046-8  
  
### 2. Construa os Containers com Docker Compose  
Com o repositório clonado, execute o seguinte comando para construir as imagens e iniciar os containers:  
  
docker-compose up --build  

Esse comando vai construir as imagens necessárias e subir os containers para os seguintes serviços:  

#### Flask (API)  
#### MariaDB (Banco de dados)  
#### Prometheus (Monitoramento)  
#### Grafana (Visualização)  
#### MySQL Exporter (Métrica para MariaDB)  

### 3. Acesse a Aplicação Web  
Após o Docker Compose concluir a construção e a inicialização dos containers, você pode acessar a aplicação através dos seguintes links:  
  
Flask (API): A aplicação Flask estará disponível em http://localhost:5000.  
Grafana: A plataforma de visualização estará disponível em http://localhost:3000. As credenciais padrão para login são:  
Usuário: admin  
Senha: admin  
Prometheus: O servidor de métricas estará disponível em http://localhost:9090.  
### 4. Acessando os Dashboards no Grafana  
Após iniciar os containers, o Grafana estará configurado para mostrar dashboards interativos. Acesse o Grafana e visualize os gráficos com métricas de desempenho, como:  
  
Métricas da aplicação Flask: Quantidade de requisições, status das requisições, latência.  
Métricas do banco de dados MariaDB: Estado do banco, tempo de resposta das queries, etc.  
### 5. Acesse o Jenkins  
O Jenkins será executado em http://localhost:8080. Faça login com as credenciais configuradas e verifique o pipeline de CI/CD, onde o código será clonado, as imagens Docker serão construídas e os testes serão executados utilizando pytest.  
  
## Jenkins - CI/CD Pipeline  
O Jenkins será utilizado para automação de integração contínua e deploy.  
  
### Acessando o Jenkins  
Acesse o Jenkins em http://localhost:8080.  
Faça login utilizando as credenciais configuradas.  
O Jenkinsfile foi configurado para:  
    Clonar o repositório.  
    Construir as imagens Docker.  
    Rodar os testes com pytest.  
    Realizar o deploy automatizado do ambiente.  
  
## Instruções de Uso  
##### Flask API  
A API Flask permite que você interaja com o banco de dados MariaDB para realizar operações de CRUD (Create, Read, Update, Delete).  
  
GET /alunos: Lista todos os alunos registrados no banco de dados.  
  
curl http://localhost:5000/alunos  
POST /alunos: Adiciona um novo aluno no banco de dados. Os dados devem ser enviados no corpo da requisição como um JSON:  
  
curl -X POST http://localhost:5000/alunos -H "Content-Type: application/json" -d '{"nome": "João", "idade": 25}'  
  
## Grafana  
O Grafana foi configurado para monitorar métricas da aplicação Flask e do banco de dados MariaDB. Você pode visualizar gráficos interativos que mostram:  
  
##### Quantidade de requisições HTTP.  
##### Latência das requisições.  
##### Status das requisições (sucesso, erro).  
##### Métricas do banco de dados, como tempo de execução das queries.  
  
## Prometheus  
O Prometheus coleta as métricas da aplicação e do banco de dados. As métricas podem ser visualizadas diretamente no Prometheus em http://localhost:9090, onde você pode realizar consultas de métricas detalhadas.  

