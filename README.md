# Task Manager API

API REST completa para gerenciamento de tarefas, desenvolvida com **FastAPI**, **PostgreSQL**, **Docker** e autenticação **JWT**.

## Tecnologias

- **FastAPI** — framework web assíncrono
- **PostgreSQL** — banco de dados relacional
- **SQLAlchemy** (async) — ORM
- **Alembic** — migrations de banco
- **JWT** — autenticação stateless
- **Docker + Docker Compose** — containerização
- **pytest** — testes automatizados
- **GitHub Actions** — CI/CD

## Funcionalidades

- Registro e login de usuários com JWT
- CRUD completo de tarefas
- Filtros por status, prioridade e conclusão
- Paginação de resultados
- Proteção de rotas (BOLA — cada usuário só acessa suas tarefas)
- Testes de integração com cobertura

## Como rodar

### Com Docker (recomendado)

```bash
# 1. Clone o repositório
git clone https://github.com/GabrielBorges240/task-manager-api.git
cd task-manager-api

# 2. Suba os containers
docker-compose up -d

# 3. Rode as migrations
docker-compose exec api alembic upgrade head

# 4. Acesse a documentação
# http://localhost:8000/docs
```

### Sem Docker

```bash
# 1. Crie o ambiente virtual
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# 2. Instale as dependências
pip install -r requirements.txt

# 3. Configure as variáveis de ambiente
cp .env.example .env
# edite o .env com suas credenciais

# 4. Rode as migrations
alembic upgrade head

# 5. Inicie a API
uvicorn app.main:app --reload
```

## Endpoints

### Autenticação

| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/auth/registro` | Criar nova conta |
| POST | `/auth/login` | Fazer login e obter token |

### Usuários

| Método | Rota | Descrição |
|--------|------|-----------|
| GET | `/usuarios/me` | Ver meu perfil |
| PATCH | `/usuarios/me` | Atualizar meu perfil |

### Tarefas

| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/tarefas` | Criar tarefa |
| GET | `/tarefas` | Listar minhas tarefas |
| GET | `/tarefas/{id}` | Buscar tarefa por ID |
| PATCH | `/tarefas/{id}` | Atualizar tarefa |
| DELETE | `/tarefas/{id}` | Deletar tarefa |

#### Query params disponíveis em GET /tarefas

- `pagina` — número da página (default: 1)
- `limite` — itens por página (default: 20, max: 100)
- `status` — `pendente` | `em_progresso` | `concluida`
- `prioridade` — `baixa` | `media` | `alta`
- `concluida` — `true` | `false`

## Exemplo de uso

```bash
# Registrar
curl -X POST http://localhost:8000/auth/registro \
  -H "Content-Type: application/json" \
  -d '{"nome": "Ana", "email": "ana@exemplo.com", "senha": "senha123"}'

# Login
curl -X POST http://localhost:8000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "ana@exemplo.com", "senha": "senha123"}'

# Criar tarefa (use o token retornado no login)
curl -X POST http://localhost:8000/tarefas \
  -H "Authorization: Bearer SEU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"titulo": "Estudar FastAPI", "prioridade": "alta"}'
```

## Testes

```bash
pip install aiosqlite pytest-asyncio
pytest tests/ -v --cov=app --cov-report=term-missing
```

## Estrutura do projeto

```
task-manager-api/
├── app/
│   ├── main.py           # ponto de entrada
│   ├── config.py         # variáveis de ambiente
│   ├── database.py       # conexão assíncrona
│   ├── models/           # tabelas do banco
│   ├── schemas/          # validação Pydantic
│   ├── repositories/     # acesso ao banco
│   ├── routers/          # rotas HTTP
│   └── services/         # lógica (auth, JWT)
├── tests/
│   ├── conftest.py       # fixtures
│   └── integration/      # testes de API
├── alembic/              # migrations
├── Dockerfile
├── docker-compose.yml
└── .github/workflows/    # CI/CD
```

## Autor

Gabriel Borges — [@GabrielBorges240](https://github.com/GabrielBorges240)
