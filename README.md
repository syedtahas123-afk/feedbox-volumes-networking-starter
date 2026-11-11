# FeedBox volumes and networking starter

FeedBox is a minimal feedback collector with PostgreSQL (`db`), Express (`api`), and an Nginx-served frontend (`web`).

## Run the project

```bash
cp .env.example .env
docker compose up --build
```

- API: http://localhost:5000/api/messages
- Frontend: http://localhost:3000

PostgreSQL data is stored in the named `postgres_data` volume. The `web` service can reach the API over the `frontend` network, while the API reaches PostgreSQL over the isolated `data` network.

For development, Docker Compose automatically reads `docker-compose.override.yml`, which mounts the API source and runs nodemon.

## Useful commands

```bash
docker compose config -q
docker compose up --build
docker compose down
docker compose down -v # removes persisted database data
```

Do not commit `.env` or `node_modules`.
