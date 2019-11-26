# Docker Cheat Sheet

This repo is used as a point of reference while doing DevOps.

- An **Image** is the application we want to run.
- A **Container** is an instance of a running image.

Run these command from a terminal. The docker commandline structure is as follows.

```bash
docker <command> <sub-command> (options)
```

## Get Docker version

To get docker version

```console
root@localhost:~$ docker -v
Docker version 18.06.1-ce, build e68fc7a
```

## Get Docker Info

To get docker info on how it has been configured

```console
root@localhost:~$ docker info
...
```

## Running\Starting a Container

To run a container (Brand New Container)

```console
root@localhost:~$ docker container run
```

To start a container (Already existing container)

```console
root@localhost:~$ docker container start <container-name-or-id>
```

### Example 1 (Running Nginx container in forground)

```console
root@localhost:~$ docker container run -p 80:80 nginx
...
```

### Example 2 (Running Nginx detatched container)

This command will give back the container ID

```console
root@localhost:~$ docker container run -p 80:80 -d nginx
9034340934e328fo828c42823093b
```

### Example 3 (Running Nginx detatched & named container)

This command will give back the container ID

```console
root@localhost:~$ docker container run -p 80:80 -d --name webhost nginx
9034340934e328fo828c42823093b
```

### Example 3 (Running Nginx interactively & named container)

This command will give back the container ID

```console
root@localhost:~$ docker container run -p 80:80 -it --name webhost nginx
9034340934e328fo828c42823093b
```

## Get list of Containers

### Running Containers

```console
root@localhost:~$ docker container ls
```

### All Containers

```console
root@localhost:~$ docker container ls -a
```

## Stop Containers

To stop a running container

```console
root@localhost:~$ docker container stop <container-id-or-name>
```

## View Running Container Logs

To view logs in a running container

```console
root@localhost:~$ docker container logs <container-id-or-name>
```

## View Running Processes in Container

To view processes in a running container

```console
root@localhost:~$ docker container top <container-id-or-name>
```

## Remove\Delete containers

To get rid of containers. For this command you can chain the container identifier in order to remove multiple containers at once.

```console
root@localhost:~$ docker container rm <container-id-or-name>
```

## Remove\Delete all stopped containers

To remove all stopped containers use the docker container prune command.

```console
root@localhost:~$ docker container prune
```

### Remove\Delete multiple containers

```console
root@localhost:~$ docker container rm <container-id-or-name> <container2-id-or-name>
```

### Remove Dangling Images

A dangling image is an image that is not tagged and is not used by any container. To remove dangling images, use:

```console
root@localhost:~$ docker rmi -f $(docker images -f dangling=true -q)
```

OR

```console
root@localhost:~$ docker image prune
```

### Remove All Unused Images

To remove all images which are not referenced by any existing container, not just the dangling ones, use the prune command with the -a flag:

```console
root@localhost:~$ docker image prune -a
```

## Bash Into A Running Container

To bash(ssh) into a running container

```console
root@localhost:~$ docker container exec -it <container-id-or-name> bash
```

### For Alpine Images

These is no bash installed on Alpine images. It has to be installed manually.

```console
root@localhost:~$ docker container exec -it <container-id-or-name> sh
```

## Pull Image From Registry\Repository

To bash(ssh) into a running container

```console
root@localhost:~$ docker pull <image-name>:<optional-tag>
```

## Get IP Address From Container

On **linux** use single quote and on **windows** use double quotes.

```console
root@localhost:~$ docker container inspect --format "{{ .NetworkSettings.IPAddress }}" <container-id-or-name>
127.0.0.1
```
