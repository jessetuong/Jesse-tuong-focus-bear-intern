## Benefits of running PostgreSQL in a Docker container

- No need to install Postgres directly on your machine — avoids version conflicts with other projects that might need a different Postgres version
- Spin up/tear down a clean database instantly for testing, without affecting a "real" local install
- Matches production environment exactly if production also runs Postgres in a container, reducing environment-specific bugs
- Easy to share the exact same DB setup with teammates via docker-compose.yml — everyone gets an identical database with one command

## How Docker volumes help persist PostgreSQL data

- By default, data written inside a container is lost if the container is removed
- Mounting a volume (e.g., postgres_data:/var/lib/postgresql/data in docker-compose.yml) stores the actual database files outside the container's writable layer, on the host (or a Docker-managed volume)
- This means you can stop, remove, and recreate the Postgres container, and reattach the same volume

## How to connect to a running PostgreSQL container

- From inside the container:
docker exec -it <container_name> psql -U <username> -d <database_name>
- From your host machine (if the container's port 5432 is published, e.g. -p 5432:5432), connect with any Postgres client using localhost and the mapped port:
psql -h localhost -p 5432 -U <username> -d <database_name>
- Or connect via a GUI tool (TablePlus, DBeaver, pgAdmin) using host localhost, port 5432 (or whatever's mapped), and the credentials set in your docker-compose.yml/environment variables