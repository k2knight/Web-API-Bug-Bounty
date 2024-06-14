# Docker

```
Here's an Beginner's Guide, along with useful commands and their usage 👩‍💻:

1. Docker Installation:
   - Install Docker from the official website according to your operating system.

2. Docker Basics:
   - docker version: Show Docker version information.
   - docker info: Display system-wide information about Docker.
   - docker help: List available Docker commands.
   - docker COMMAND --help: Get help for a specific Docker command.

3. Docker Images:
   - docker images: Show all the available local Docker images.
   - docker pull IMAGE_NAME:TAG: Fetch an image from a repository.
   - docker build -t IMAGE_NAME:TAG DOCKERFILE_DIR: Build an image from a Dockerfile.
   - docker push IMAGE_NAME:TAG: Push an image to a registry/repository.
   - docker rmi IMAGE_NAME:TAG: Remove a specific image from the local machine.
   - docker rmi $(docker images -q): Remove all local Docker images.

4. Docker Containers:
   - docker run IMAGE_NAME:TAG: Create and start a new container.
   - docker start CONTAINER_ID/NAME: Start an existing container.
   - docker stop CONTAINER_ID/NAME: Stop a running container.
   - docker restart CONTAINER_ID/NAME: Restart a container.
   - docker rm CONTAINER_ID/NAME: Remove a specific container.
   - docker ps: List running containers.
   - docker ps -a: List all containers (including stopped ones).
   - docker exec -it CONTAINER_ID/NAME COMMAND: Execute a command inside a running container.
   - docker logs CONTAINER_ID/NAME: Show the logs of a container.

5. Docker Volumes:
   - docker volume create VOLUME_NAME: Create a named volume.
   - docker volume ls: Show available volumes.
   - docker run -v VOLUME_NAME:CONTAINER_PATH IMAGE_NAME: Mount a volume to a container.
   - docker volume rm VOLUME_NAME: Remove a specific volume.

6. Docker Networks:
   - docker network create NETWORK_NAME: Create a user-defined network.
   - docker network ls: List available networks.
   - docker run --network NETWORK_NAME IMAGE_NAME: Attach a container to a network.
   - docker network rm NETWORK_NAME: Remove a specific network.

7. Docker Compose:
   - docker-compose up: Start containers defined in a compose file.
   - docker-compose down: Stop and remove containers defined in a compose file.
   - docker-compose logs SERVICE_NAME: Show logs for a specific service.

These commands should give you a good starting point for using Docker efficiently. You can explore each command further by referring to the Docker documentation.

Uploaded By - @MADARA888UCHIHAA ⚡
```