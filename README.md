# Task Manager API

A production-ready RESTful API for task management, built with FastAPI, PostgreSQL, Docker, and JWT authentication. The project follows modern backend development practices, including asynchronous database operations, automated testing, database migrations, and CI/CD integration.

## Technologies

* **FastAPI** — High-performance asynchronous web framework
* **PostgreSQL** — Relational database management system
* **SQLAlchemy (Async)** — Asynchronous ORM
* **Alembic** — Database migration management
* **JWT** — Stateless authentication and authorization
* **Docker & Docker Compose** — Containerization and orchestration
* **Pytest** — Automated testing framework
* **GitHub Actions** — Continuous Integration and Deployment (CI/CD)

## Features

* User registration and authentication with JWT
* Full CRUD operations for task management
* Filtering by status, priority, and completion state
* Pagination support for scalable data retrieval
* Route protection and user-based resource ownership (BOLA prevention)
* Integration tests with coverage reporting
* Modular and scalable architecture

## Getting Started

### Using Docker (Recommended)

```bash
git clone https://github.com/GabrielBorges240/task-manager-api.git
cd task-manager-api

docker-compose up -d

docker-compose exec api alembic upgrade head
```

API Documentation:

```text
http://localhost:8000/docs
```

### Local Development

```bash
python -m venv venv

# Linux / macOS
source venv/bin/activate

# Windows
venv\Scripts\activate

pip install -r requirements.txt

cp .env.example .env

alembic upgrade head

uvicorn app.main:app --reload
```

## API Endpoints

### Authentication

| Method | Endpoint         | Description                             |
| ------ | ---------------- | --------------------------------------- |
| POST   | `/auth/register` | Create a new account                    |
| POST   | `/auth/login`    | Authenticate and obtain an access token |

### Users

| Method | Endpoint    | Description                   |
| ------ | ----------- | ----------------------------- |
| GET    | `/users/me` | Retrieve current user profile |
| PATCH  | `/users/me` | Update current user profile   |

### Tasks

| Method | Endpoint      | Description         |
| ------ | ------------- | ------------------- |
| POST   | `/tasks`      | Create a new task   |
| GET    | `/tasks`      | Retrieve user tasks |
| GET    | `/tasks/{id}` | Get a task by ID    |
| PATCH  | `/tasks/{id}` | Update a task       |
| DELETE | `/tasks/{id}` | Delete a task       |

## Testing

```bash
pytest tests/ -v --cov=app --cov-report=term-missing
```

## Project Structure

```text
task-manager-api/
├── app/
│   ├── main.py
│   ├── config.py
│   ├── database.py
│   ├── models/
│   ├── schemas/
│   ├── repositories/
│   ├── routers/
│   └── services/
├── tests/
├── alembic/
├── Dockerfile
├── docker-compose.yml
└── .github/workflows/
```

## Author

**Gabriel Borges**

Backend Developer focused on scalable APIs, software architecture, and AI-powered applications.
