## docker run vs. docker-compose up

- docker run starts a single container from a single image while docker-compose up reads a docker-compose.yml file and starts multiple containers listed in the file together, with their configuration, networking, and dependencies already defined declaratively, which means users will not have to write multiple docker run commands
- compose also handles cross-container networking and relationship, for example: backend container can reach a database container by service name

## How Docker Compose helps with multiple services

- Defines an entire stack (backend, database,..) in one YAML file, version-controlled alongside the code
- Starts/stops all services together with a single command (docker-compose up / down)
- Manages shared networks so services can connect to each other without human manual config
- Makes it easy to reproduce the exact same multi-service environment on any machine

## Commands to check logs

- docker logs <container_name_or_id>           # check logs for a container
- docker logs -f <container_name_or_id>       # follow/stream logs live
- docker-compose logs                          # logs for all containers in the stack
- docker-compose logs -f <service_name>        # follow logs for one service

## What happens when you restart a container — does data persist?

- docker restart <container> stops and starts the same container — any data written inside the container's writable layer is preserved, since it's the same container instance      
- However, if the container is removed (docker rm) and a new one is created from the image, any data in that container will be removed
- Data only reliably persists across container recreation if it's stored in a Docker volume or bind mount, which lives outside the container's lifecycle