# intelowl Devcontainer Setup

This folder contains the complete development container configuration for intelowl.

## Files Created

### Core Devcontainer Files
- `devcontainer.json` - Main devcontainer configuration
- `Dockerfile` - Python development environment
- `docker-compose.yml` - Support services (postgres, rabbitmq, nginx)
- `nginx.conf` - Nginx configuration for development

### VSCode Configuration
- `.vscode/launch.json` - Debug configurations for Django and Celery
- `.vscode/tasks.json` - Service management tasks
- `.vscode/settings.json` - VSCode settings and preferences

## Key Features

1. **Complete Isolation**: All dev config in `.devcontainer/` folder
2. **Zero Repo Changes**: Original intelowl code remains untouched
3. **Full Debugging Support**: Django and Celery worker debugging
4. **Service Integration**: PostgreSQL, RabbitMQ, Nginx containers
5. **Localhost ES Access**: Containers can reach Elasticsearch on host
6. **VSCode Integration**: Extensions, linting, formatting pre-configured

## Usage

1. Open intelowl repo in VSCode
2. When prompted, select "Reopen in Container"
3. VSCode will build the devcontainer and start services
4. Use debug configurations to start Django/Celery with debugging

## Debug Configurations

- **Django: Run Server** - Start Django with debugging
- **Django: Migrations** - Run database migrations
- **Celery: Worker** - Start Celery worker with debugging
- **Celery: Beat** - Start Celery beat scheduler
- **Django: Test** - Run Django tests

## Networking

- Containers use `intelowl-dev` network
- `host.docker.internal` allows access to localhost services
- Elasticsearch on localhost:9200 accessible from containers

## Environment Variables

All necessary environment variables are pre-configured for development, including database connections, RabbitMQ settings, and Elasticsearch host configuration.