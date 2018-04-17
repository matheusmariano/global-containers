# Global Containers

Provide Docker containers for common services.

## Getting Started

Clone this repository in your machine then run the services you want using **Docker Compose**.

```
docker-compose up -d postgres redis
```

## Configuration

Environment variables can be set inside service's folder, inside `.env` files.

## Import existing Postgres databases

If you have old databases, you can import them to Docker generating a SQL file.

```
pg_dumpall -U <username> > postgres/home/db.sql
```

Add the following volume to your Postgres service in `docker-compose.yml`.

```
- ./postgres/home:/home
```

Now you must get the running Postgres container ID.

```
docker container ls
```

This command will return something like


```
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS                    NAMES
d0c128d4c488        postgres:10.3-alpine   "docker-entrypoint..."   3 hours ago         Up 3 hours          0.0.0.0:5432->5432/tcp   globalcontainers_postgres_1
```

Run the command bellow with your container ID.

```
docker exec -it <container-id> psql -U <username> -f /home/db.sql
```

If the databases were imported successfully, you may remove the volume inserted above from `docker-compose.yml`.

## Special Containers

### Redsmin

Redsmin is an online Redis manager.

To run this service, you must have an account in [redsmin.com](https://www.redsmin.com) and add your `REDIS_URL` and `REDSMIN_KEY` inside `redsmin-proxy/.env` file and execute

```
docker-compose up redsmin-proxy
```

## License

Global Containers is open-sourced software licensed under the MIT license.
