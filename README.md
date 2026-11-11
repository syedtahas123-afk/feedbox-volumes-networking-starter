# FeedBox volumes and networking

FeedBox is a minimal feedback collector with PostgreSQL (`db`), Express (`api`), and an Nginx-served frontend (`web`).

## Run the project

```bash
cp .env.example .env
docker compose up --build
```

- Frontend: http://localhost:3000
- API: http://localhost:5000/api/messages

## Docker configuration

- **Persistent database:** PostgreSQL stores its data in the named `postgres_data` volume mounted at `/var/lib/postgresql/data`. The data remains when containers are recreated. It is removed only when you explicitly run `docker compose down -v`.
- **Network isolation:** `db` is attached only to the `data` bridge network. `api` is attached to both `data` and `frontend`, allowing it to communicate with PostgreSQL and the web tier. `web` is attached only to `frontend`.
- **Development override:** `docker-compose.override.yml` runs the API with nodemon, bind-mounts the project into `/app`, and keeps container dependencies in the separate anonymous `/app/node_modules` volume so the host mount does not hide them.

Compose automatically merges the override file during normal local development.

## Validate

```bash
docker compose config -q
docker compose up --build
```

To stop containers without deleting database data:

```bash
docker compose down
```

To deliberately remove the database volume as well:

```bash
docker compose down -v
```

Copy `.env.example` to `.env` and set a local password before starting. Do not commit `.env` or `node_modules`.
