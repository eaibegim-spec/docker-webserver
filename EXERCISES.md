# Docker Compose practice

Work through these exercises in order. Write the Compose configuration yourself,
then validate it with:

```bash
docker compose config
```

## Exercise 1 — One web server

Create one Nginx service.

- Use the `nginx` image.
- Map host port `8081` to container port `80`.
- Start it with `docker compose up -d`.
- Open <http://localhost:8081>.
- Stop it with `docker compose down`.

Learn: `services`, `image`, `ports`.

## Exercise 2 — Named volume

Create a PostgreSQL service whose data survives container recreation.

- Use the `postgres` image.
- Set `POSTGRES_USER`, `POSTGRES_PASSWORD`, and `POSTGRES_DB`.
- Create a named volume.
- Mount it at `/var/lib/postgresql/data`.
- Declare the named volume in a top-level `volumes:` section.

Learn: `environment` and named volumes.

## Exercise 3 — Bind mount (current webserver)

Serve a local HTML file with Nginx.

- Create `html/index.html`.
- Mount `./html` at `/usr/share/nginx/html`.
- Edit `index.html` and refresh the browser.

Learn: bind mounts and the difference between host and container paths.

## Exercise 4 — Two connected services

Create a small web application and a database.

- Add `web` and `db` services.
- Give the application the database hostname `db`.
- Do not use a container IP address.
- Confirm that the application can reach the database.

Learn: Compose networking and service-name DNS.

## Exercise 5 — Dependencies and health checks

Make the web application wait for a healthy database.

- Add `depends_on` to `web`.
- Add a health check to `db`.
- Use `condition: service_healthy`.

Learn: a started container is not necessarily ready.

## Exercise 6 — Environment file

Move configuration out of the Compose file.

- Create a `.env` file for database values.
- Reference values with `${VARIABLE_NAME}`.
- Do not commit real passwords.

Learn: variable substitution and environment configuration.

## Exercise 7 — Custom networks

Separate public-facing and private services.

- Create `frontend` and `backend` networks.
- Connect `web` to both networks.
- Connect `db` only to `backend`.
- Optionally add Redis to `backend`.

Learn: network isolation.

## Exercise 8 — Mini stack

Build one complete stack from scratch:

- Nginx and a static website
- Node or Python API and PostgreSQL
- WordPress and MySQL
- Redis and a small API or worker

Include suitable ports, volumes, environment values, and health checks.

## Exercise 9 — Development and production files

Create different configurations for development and production.

- Keep shared settings in `compose.yaml`.
- Put local bind mounts and debug ports in `compose.override.yaml`.
- Alternatively, create `compose.prod.yaml`.

Run multiple files with:

```bash
docker compose -f compose.yaml -f compose.prod.yaml up
```

Learn: Compose file merging and overrides.

## Useful commands

```bash
docker compose config
docker compose up -d
docker compose ps
docker compose logs
docker compose down
```

Be careful with `docker compose down -v`: it also deletes named volumes and
their stored data.
