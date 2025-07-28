*------- Library API ----------*

Uma API simples para gerenciar usuários em uma biblioteca online, construída com FastAPI e Supabase. Esta API permite cadastro, login e gerenciamento de perfis de usuários (listar, obter detalhes e atualizar). Foi desenvolvida como parte de uma aula prática, com foco em autenticação e CRUD.

Nota: Durante o desenvolvimento, enfrentamos alguns desafios (como erros de configuração do Supabase e validação de tokens), mas todos foram resolvidos, e a API está funcionando corretamente!


*-------- Funcionalidades ---------*

Cadastro: Crie uma conta com email, senha, nome e função (ex.: member, admin).
Login: Autentique-se e receba um token JWT.
CRUD de Usuários:
Listar todos os perfis.
Obter detalhes de um usuário por ID.
Atualizar nome ou função do usuário.

- Documentação automática com Swagger em /docs.

*------ Tecnologias ---------*

FastAPI: Framework para criar a API.
Supabase: Banco de dados PostgreSQL e autenticação.
Pydantic: Validação de dados.
Python 3.11+: Linguagem usada.

*--------- Estrutura do Projeto -----------*

/library-api
├── /app
│   ├── main.py          # Ponto de entrada da API
│   ├── /api
│   │   ├── /v1
│   │   │   ├── auth.py  # Rotas de cadastro e login
│   │   │   ├── users.py # Rotas para gerenciar usuários
│   ├── /core
│   │   ├── config.py    # Configurações do Supabase
│   │   ├── database.py  # Conexão com o Supabase
│   ├── /models
│   │   ├── user.py      # Modelos de dados
├── .env                 # Chaves do Supabase (não versionar!)
├── requirements.txt     # Dependências
├── README.md            # Este arquivo


*---------- Pré-requisitos ---------*

Python 3.11+
Conta no Supabase (crie em supabase.com)
Git instalado


*--------- Configuração -----------*
Clone o repositório:
git clone https://github.com/seu-usuario/library-api.git
cd library-api


Crie um ambiente virtual:
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows


Instale as dependências:
pip install -r requirements.txt


Configure o Supabase:

Crie um projeto no Supabase.
Pegue a URL do projeto (ex.: https://xyz.supabase.co) e a API Key (chave "anon" em Settings > API).
Habilite autenticação por email (Dashboard > Authentication > Providers > Email).
Crie a tabela profiles no editor SQL do Supabase:CREATE TABLE profiles (
    id UUID PRIMARY KEY REFERENCES auth.users(id),
    full_name VARCHAR(255),
    role VARCHAR(50) DEFAULT 'member',
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


Crie o arquivo .env:Na raiz do projeto, crie um arquivo .env com:
SUPABASE_URL=https://xyz.supabase.co
SUPABASE_KEY=your-anon-key



*------- Como Rodar ------*

Inicie a API:
uvicorn app.main:app --reload


*------ Acesse a API: -----*

Abra http://localhost:8000/docs para ver a documentação Swagger.
Teste as rotas:
POST /api/v1/auth/signup: Cadastre um usuário (ex.: {"email": "teste@email.com", "password": "senha123", "full_name": "Teste", "role": "member"}).
POST /api/v1/auth/login: Faça login e pegue o token.
Use o token para testar as rotas /users (clique no cadeado no Swagger para autenticar).


*----- Notas sobre Desenvolvimento ---------*

Durante o desenvolvimento, enfrentamos erros como:
Configuração incorreta do Supabase (URL ou chave errada).
Problemas com validação de tokens JWT.
Erros ao mapear dados do Supabase para os modelos Pydantic.


Todos os erros foram resolvidos ajustando configurações, revisando a documentação do Supabase e testando as rotas no Swagger.
A API está estável e pronta para uso!

*------- Próximos Passos --------*

Adicionar rotas para redefinição de senha.
Implementar permissões (ex.: apenas admins listam usuários).
Adicionar funcionalidades como gerenciamento de livros.
