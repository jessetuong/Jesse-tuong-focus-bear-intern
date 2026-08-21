## How to check logs from a running container

- docker logs <container_name_or_id>              # check logs for one container
- docker logs -f <container_name_or_id>          # follow/stream in real time
- docker logs --tail 100 <container_name_or_id>  # last 100 lines only
- docker-compose logs -f <service_name>          # if using Compose

## docker exec vs docker attach

- docker exec starts a new process inside an already-running container, separate from the container's main process. You can exit it without affecting the container.
- docker attach connects directly to the container's main running process
- In real life, docker exec is used more often since it is safer to debug

## Restarting a container without losing data

- Use: docker restart <container_name>. This syntax stops and starts the same container, which preserves its data
- Data only survives container removal (for example: from docker compose down, docker rm) if it's stored in a Docker volume.

## Troubleshooting database connection issues inside a containerized NestJS app

- Check the NestJS container can reach the DB container by name: docker exec -it <nestjs_container> ping <db_service_name> (use the Compose service name, not localhost, since they're separate containers)
- Verify environment variables (DB_HOST, DB_PORT, DB_USER, DB_PASSWORD) match what's set in docker-compose.yml — a common mistake is pointing DB_HOST at localhost instead of the Postgres service name
- Confirm the Postgres container is actually healthy and accepting connections: docker logs <postgres_container> — look for "database system is ready to accept connections"
- Make sure both containers are on the same Docker network (Compose does this automatically if they're in the same docker-compose.yml)
- Try connecting manually from inside the NestJS container to isolate whether it's a networking issue or an app config issue: docker exec -it <nestjs_container> sh then attempt a connection with a Postgres client if available, or check with nc -zv <db_service_name> 5432