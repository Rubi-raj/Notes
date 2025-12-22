<p style="text-align: center;">
  <img src="https://files.svgcdn.io/logos/docker.svg" alt="Docker logo" width="250" height="100">
</p>

# What is Docker ?

Docker is a virtualization software, makes developing and deploying applications much easier.

## Docker Images Vs Containers

Images are templates for containers.

### Docker Images

- Executable application artifact
- Any services (postgres, npm, node)
- Environment variables, create directories, files etc.

### Docker Containers

- A running instance of an image is a container.
- Can run multiple containers from 1 image.

## Docker Registries

- A storage and distribution system for Docker images.
- Docker hosts one of the biggest Docker Registry, called “Docker Hub”.

---

# Docker Commands

| Command                                        | Description                      |
|------------------------------------------------|----------------------------------|
| `docker images` or `docker image ls`           | List all Docker images           |
| `docker ps`                                    | List running containers          |
| `docker pull {imageName}:{tag}`                | Pull an image from a registry    |
| `docker run {imageName}:{tag}`                 | Run a container                  |
| `docker container prune`                       | Remove all stopped containers    |
| `docker logs {containerId/name}`               | View logs from container         |
| `docker stop {containerId/Name}`               | Stop running container           |
| `docker exec -it {containerId/Name} /bin/bash` | Open inside a container to debug |

---

# Docker Run Commands

```bash
docker run -d -p {hostPort}:{containerPort} -e {key}={value} --name {containerName} --rm {imageName}:{tag}
```

- `-d` Run container in background and print container ID
- `-p {hostPort}:{containerPort}` Publish a container's port to the host
- `-e {key}={value}` Environment variable
- `--name {containerName}` Assign a name to the container
- `--rm` Delete the container once it stop

---

# Slim & Alphine Images

| Slim               | Alphine                 |
|--------------------|-------------------------|
| Small image        | Typically smaller image |
| Debian-based Linux | Alpine Linux            |

---

# Docker Mounts

- Volumes
- Bind-mounts
- Tempfs mounts <br>
  `docker run -v {/path/in/host}:{/path/in/container} {imageName}:{tag}`
