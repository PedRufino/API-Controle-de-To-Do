# API de Controle de To-Do com PostgreSQL e Docker
Neste repositório, você encontrará uma API que foi desenvolvida para o controle de tarefas (To-Do) com funcionalidades para adicionar, editar, excluir e listar tarefas.

## Descrição
A API retorna dados em formato JSON, incluindo informações como título, descrição e status (done). Além disso, para armazenar os dados de forma segura e eficiente, o PostgreSQL foi utilizado como banco de dados, e o Docker foi empregado para criar um contêiner do PostgreSQL. Isso permite que você inicie facilmente um ambiente de banco de dados em contêiner, tornando o desenvolvimento e implantação mais ágeis e escaláveis.

## Informações do Projeto

#### O que foi utilizado:
- Go (Golang)
- Docker

#### Configurações para o funcionamento do projeto

\* Dentro do projeto execute os comandos a baixo para o funcionamento do mesmo<br>
```sh
go run main.go
```

#### (opcional) Configurações para a criar o contêiner do PostgreSQL

```sh
# Crie o container do PostgreSQL
docker run -d --name api-todo -p 5432:5432 -e POSTGRES_PASSWORD=1234 postgres:13.5

# Execute o container em segundo plano e conecta no banco de dados
docker exec -it api-todo psql -U postgres

# Crie um usuario
create user user_todo;

# Adicione uma senha
alter user user_todo with encrypted password '1122';
 
# Crie o Banco de Dados 
create database api_todo;
 
# Adicione privilegios
grant all privileges on database api_todo to user_todo;
 
# Acesse o Banco de Dados
\c api_todo
 
# (opcional) Verifique as tabelas existentes
\dt
 
# Crie uma Tabela no Banco
create table todos (id serial primary key, title varchar, description text, done bool default FALSE);
 
# Adicione privilegios
grant all privileges on all tables in schema public to user_todo;
grant all privileges on all sequences in schema public to user_todo;
```
## Observações

Para prosseguir com a configuração, é necessário ter o Docker instalado. Se você ainda não possui o Docker, você pode encontrar instruções detalhadas de instalação no site oficial, disponíveis no seguinte link: [Link para o site oficial de instalação do Docker](https://docs.docker.com/desktop/).

Caso você já tenha o PostgreSQL instalado em sua máquina, você só precisará realizar as seguintes etapas:

1. Crie a base de dados necessária.
2. Crie as tabelas conforme especificado.
3. Adicione as informações do seu host, usuário, senha e nome da base de dados ao arquivo `config.toml`.
