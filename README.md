## Dev workflow

### Run during development

From a root directory of project run command.

#### First run. It runs all related services, migrates a database and seeds the data.

```bash
docker compose -f docker-compose.yml --env-file .env.dev -p net8test up --build --remove-orphans
```

#### Stop and remove all services

```bash
docker compose -f docker-compose.yml --env-file .env.dev -p net8test down
```

## Build and publish container

```bash
docker buildx create --use --bootstrap && \
docker buildx build --platform linux/amd64,linux/arm64 --build-arg BUILD_CONFIGURATION=Debug --push -t sucasuc.azurecr.io/net8test:v1.0.4 -f ./WebApplication11Api/Dockerfile .
```

where `v1.0.3` is a version of a container