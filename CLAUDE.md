# 🤖 CLAUDE.md — api-ecommerce

> Context for Claude Code. Read it before working on this project.

## 📋 Description

Backend API RESTful using .NET9

## 🗂️ Category

learning

## 🛠️ Stack

<!-- Describe the technologies used by the project here -->
- .NET 9 (ASP.NET Core)
- SQL Server 2022 (Developer edition)
- Dev Containers (Docker Compose)

## 📁 Structure

```
api-ecommerce/
├── .devcontainer/
│   ├── devcontainer.json
│   ├── docker-compose.yml
│   └── .env.example
├── CLAUDE.md
├── README.md
├── .editorconfig
└── .gitignore
```

## 🐳 Docker

The environment runs as a Dev Container defined in `.devcontainer/`:

| Service / container  | Image                                         | Role                          |
| -------------------- | --------------------------------------------- | ----------------------------- |
| `api-ecommerce-app`  | `mcr.microsoft.com/devcontainers/dotnet:2-9.0` | .NET 9 dev workspace          |
| `api-ecommerce-db`   | `mcr.microsoft.com/mssql/server:2022-latest`   | SQL Server, `127.0.0.1:1433`  |

Setup:

```bash
cp .devcontainer/.env.example .devcontainer/.env   # then set MSSQL_SA_PASSWORD
```

Then in VS Code: **Dev Containers: Reopen in Container**. To manage it manually:

```bash
# Start
docker compose -f .devcontainer/docker-compose.yml up -d

# View logs
docker compose -f .devcontainer/docker-compose.yml logs -f

# Stop
docker compose -f .devcontainer/docker-compose.yml down
```

- From inside the app container the DB host is `api-ecommerce-db` (not `localhost`); from the host machine use `localhost,1433`.
- The connection string is injected as `ConnectionStrings__DefaultConnection` → read it with `GetConnectionString("DefaultConnection")`.
- DB data persists in the named volume `api-ecommerce-db-data` (`docker volume rm api-ecommerce-db-data` to reset the DB).
- The app container waits for the DB healthcheck (`sqlcmd SELECT 1`) before starting.

## 🔧 Conventions

- File names: kebab-case
- Indentation: tabs of 4 (see `.editorconfig`; YAML and Markdown use 2 spaces)
- Commits: in English, descriptive
- Branches: `feature/name`, `fix/name`, `hotfix/name`, `docs/name`, `refactor/name`, `chore/name`, `style/name`

## ⚠️ Important notes

<!-- Add things Claude should know here: test credentials, limitations, etc. -->
- `.gitignore` starts empty: update it to match the project's stack
- Never commit `.devcontainer/.env` (ignored by the `.env` rule); add new variables to `.devcontainer/.env.example`

## 📌 Current status

<!-- Update this when you pause work -->
- Last task: Dev Container setup (.NET 9 + SQL Server 2022) with DB healthcheck and env-based credentials
- Next step: scaffold the ASP.NET Core Web API project
