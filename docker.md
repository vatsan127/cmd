## _Version_

```
docker --version
```

---

## _Containers_

List all currently running containers.

```
docker ps
```

List all containers, including those that are stopped.

```
docker ps -a
```

Run Docker Container

```
docker run <image_name>
```

Run a container in interactive mode with a bash shell.

```
docker run -it <image_name> /bin/bash
```

Stop Docker Container

```
docker stop <container_id>
```

Remove Docker Container

```
docker rm <container_id>
```

---

## _Images_

List all Docker images on your local system.

```
docker images
```

Download a Docker image from Docker Hub to your local system.

```
docker pull <image_name>
```

Remove Docker Image

```
docker rmi <image_id>
```

Build Docker Image from Dockerfile

```
docker build -t <image_name>:<tag> .
```

Tag Docker Image

```
docker tag <existing_image> <new_image>
```

Push Docker Image to Repository

```
docker push <repository>/<image_name>:<tag>
```

DockerHub Login

```
docker login
```

---

## _Networks_

Lists all Docker networks.

```
docker network ls
```

Create Docker Network

```
docker network create <network_name>
```

Connect Container to Network

```
docker network connect <network_name> <container_id>
```

Disconnect Container from Network

```
docker network disconnect <network_name> <container_id>
```

---

## _Volumes_

Lists all Docker volumes.

```
docker volume ls
```

Create Docker Volume

```
docker volume create <volume_name>
```

Inspect Docker Volume

```
docker volume inspect <volume_name>
```

Remove Docker Volume

```
docker volume rm <volume_name>
```