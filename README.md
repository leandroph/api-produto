# Projeto Api Produto

## Requisitos do Projeto:

Antes de começar, você vai precisar ter instalado em sua máquina os seguintes recursos:

- [Git](https://git-scm.com/downloads)
- [Docker](https://docs.docker.com/get-docker/)

## Executando o Projeto:

Para testarmos a aplicação, temos que executar os 4 passos a seguir:

1. [Fazer download do Projeto](#download-github)
2. [Criar containers com Docker CLI](#criar-cli)
3. [Criar containers com Docker Compose](#criar-compose)

<a name="download-github"></a>
### 1. Fazer download do do Projeto:
 1. Baixe este Repositório, executando o comando Git:
```bash
git clone https://github.com/leandroph/api-produto.git
```

<a name="criar-cli"></a>
### 2. Criar containers com Docker CLI:

 1. Criar volume para salvar base do mongo:
 ```bash
 docker volume create mongo_vol
 ```
 
 2. Criar uma rede para conectar os containes:
 ```bash
 docker network create produto_net
 ```
 
 3. Fazer o build da imagem, no diretório `src`:
 ```bash
 docker build -t lheck/api-produto:v1 .
 ```
 
 - <b>Obs.:</b> Você terá uma resposta semelhante ao texto abaixo:
 ```bash
 REPOSITORY              TAG       IMAGE ID       CREATED          SIZE
 lheck/api-produto       v1        eadb90d16e58   11 seconds ago   985MB
 ```
 
 4. Criar o container do MongoDB:
 ```bash
 docker container run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=mongouser -e MONGO_INITDB_ROOT_PASSWORD=mongopwd -v mongo_vol:/data/db --network produto_net --name mongodb mongo:4.4.3
 ```
 
 5. Criar o container da Api Produto, imagem que foi realizado o build:
 ```bash
 docker container run -d -p 8080:8080 --network produto_net -e MONGODB_URI=mongodb://mongouser:mongopwd@mongodb:27017/admin lheck/api-produto:v1
 ```
 
 <a name="criar-"><compose/a>
### 3. Criar containers com Docker Compose:

 1. No diretório raiz, executar o docker compose:
 ```bash
 docker-compose up -d
 ```
