# Docker

## Version

```sh
docker --version
```

---

## Images

### Inspect

List all Docker images on your local system.

```sh
docker images
```

### Build & Pull

Download an image from Docker Hub to your local system.

```sh
docker pull <image_name>
```

Build an image from a Dockerfile.

```sh
docker build -t <image_name>:<tag> .
```

### Publish

Log in to Docker Hub.

```sh
docker login
```

Tag an image.

```sh
docker tag <existing_image> <new_image>
```

Push an image to a repository.

```sh
docker push <repository>/<image_name>:<tag>
```

### Remove

Remove an image.

```sh
docker rmi <image_id>
```

---

## Containers

### Run

Run a container.

```sh
docker run <image_name>
```

Run a container in interactive mode with a bash shell.

```sh
docker run -it <image_name> /bin/bash
```

### Inspect

List all currently running containers.

```sh
docker ps
```

List all containers, including those that are stopped.

```sh
docker ps -a
```

### Stop & Remove

Stop a container.

```sh
docker stop <container_id>
```

Remove a container.

```sh
docker rm <container_id>
```

---

## Networks

List all Docker networks.

```sh
docker network ls
```

Create a network.

```sh
docker network create <network_name>
```

Connect a container to a network.

```sh
docker network connect <network_name> <container_id>
```

Disconnect a container from a network.

```sh
docker network disconnect <network_name> <container_id>
```

---

## Volumes

List all Docker volumes.

```sh
docker volume ls
```

Create a volume.

```sh
docker volume create <volume_name>
```

Inspect a volume.

```sh
docker volume inspect <volume_name>
```

Remove a volume.

```sh
docker volume rm <volume_name>
```
