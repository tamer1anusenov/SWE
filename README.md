# Supplier Sales Rep System (Mobile Web + Backend)

This repository contains:

- **Backend API** – FastAPI + PostgreSQL + SQLAlchemy (async) + Alembic  
- **Mobile App (Web)** – Flutter Web build of the Supplier Sales Representative app  
- **Dockerized Infrastructure** – Backend, database, and mobile web app running via `docker compose`

---

## 👥 Team Members

- **Damir Kushumbayev**  
- **Arnal Beisenov**  
- **Tamerlan Ussenov**  
- **Ayaulym Zhumagul**

---

## 📁 Project Structure

```text
project-root/
│
├── backend/
│   ├── app/
│   ├── alembic/
│   ├── alembic.ini
│   ├── requirements.txt
│   ├── Dockerfile
│   └── .dockerignore
│
├── mobile/
│   ├── android/
│   ├── ios/
│   ├── lib/
│   ├── web/
│   ├── pubspec.yaml
│   ├── Dockerfile.web
│   └── .dockerignore
│
├── docker-compose.yml
└── .env
```

✅ Requirements
Docker (20+)

Docker Compose (v2+)

You do not need local Python, Flutter, or PostgreSQL to run the stack – everything runs inside Docker.

⚙️ Environment Configuration
Create a .env file in the project root (same level as docker-compose.yml):

env
Copy code
# --- Postgres ---
POSTGRES_USER=tamerlan
POSTGRES_PASSWORD=123
POSTGRES_DB=scp_db

# --- Backend runtime ---
DATABASE_URL=postgresql+asyncpg://tamerlan:${POSTGRES_PASSWORD}@postgres:5432/${POSTGRES_DB}

SECRET_KEY=your_secret_key_here
ACCESS_TOKEN_EXPIRE_MINUTES=30
REFRESH_TOKEN_EXPIRE_MINUTES=43200

ENVIRONMENT=development
DEBUG=True
HOST=0.0.0.0
PORT=8000
❗ Important:

DATABASE_URL must use postgres as host (the Docker service name), not localhost.

🚀 How to Run the Project
1️⃣ Build and Start All Services
From the project root:

bash
Copy code
docker compose up --build
This will start:

postgres – PostgreSQL database

backend – FastAPI application on port 8000

mobile_web – Flutter Web app served by Nginx on port 50000

2️⃣ Apply Database Migrations (Alembic)
Migrations are not run automatically (by design).

After containers are up:

bash
Copy code
docker exec -it backend alembic upgrade head
This will apply all Alembic migrations to the scp_db database.

🌐 URLs
Once everything is running:

Mobile Web App (Flutter)
http://localhost:50000

Backend API Docs (FastAPI / Swagger UI)
http://localhost:8000/docs

OpenAPI JSON
http://localhost:8000/openapi.json

Common Docker Commands
Rebuild images after code changes
```
docker compose up --build
```
Run in background (detached mode)
```
docker compose up -d
```

Stop all services
bash
Copy code
docker compose down
View logs (all services)
bash
Copy code
docker compose logs -f
View logs for a specific service
bash
Copy code
docker compose logs -f backend
docker compose logs -f mobile_web
docker compose logs -f postgres
🧩 Tech Stack Summary
Backend

Python 3.12

FastAPI

SQLAlchemy 2 (async) + asyncpg

Alembic (migrations)

JWT auth (python-jose, passlib[bcrypt])

Pydantic / pydantic-settings

Uvicorn (ASGI server)

Mobile (Web)

Flutter Web

Built in Docker, served by Nginx

Reverse proxy from / → Flutter app, /api/ → backend (service backend:8000)

🛠 Development Notes
For local (non-Docker) dev, you can still run:

Backend: uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

Database: connect to PostgreSQL using the same user/db as in .env

Make sure your Flutter app uses a configurable API base URL (e.g. via --dart-define=API_URL=...) so it can point to http://backend:8000 inside Docker.

# Supplier Sales Rep System  
### (Flutter Mobile Web + FastAPI Backend + PostgreSQL)

This repository hosts the full system for the **Supplier Sales Representative** workflow, including:

- **Backend API** – FastAPI + PostgreSQL + SQLAlchemy (async)
- **Mobile App (Web Version)** – Flutter Web build served via Nginx
- **Dockerized Infrastructure** – Backend, DB, and mobile web app running together using Docker Compose

---

## 👥 Team Members

- **Damir Kushumbayev**
- **Arnal Beisenov**
- **Tamerlan Ussenov**
- **Ayaulym Zhumagul**

---

## 📁 Project Structure

project-root/
│
├── backend/
│ ├── app/
│ ├── alembic/
│ ├── alembic.ini
│ ├── requirements.txt
│ ├── Dockerfile
│ └── .dockerignore
│
├── mobile/
│ ├── android/
│ ├── ios/
│ ├── lib/
│ ├── web/
│ ├── pubspec.yaml
│ ├── Dockerfile.web
│ └── .dockerignore
│
├── docker-compose.yml
└── .env

yaml
Copy code

---

## 🛠 Technology Stack

### Backend
- Python 3.12  
- FastAPI  
- SQLAlchemy 2 (async)  
- asyncpg (PostgreSQL driver)  
- Alembic (migrations)  
- JWT Auth (`python-jose`, `passlib[bcrypt]`)  
- Pydantic & pydantic-settings  
- Uvicorn ASGI Server  

### Mobile Web (Frontend)
- Flutter Web  
- Nginx (static hosting + proxy to backend)  
- API routing `/api` → backend container  


