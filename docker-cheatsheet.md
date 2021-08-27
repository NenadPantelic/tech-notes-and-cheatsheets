# Docker cheatsheet

## 1. Container related commands

### 1. Run a container in interactive mode

```bash
# run a bash shell inside container
docker run -it <container-name> bash
```

### 2. Run a container in detached mode

```bash
# container name - mywildfly
# -d => detached mode (doesn't occupy terminal session)
# 8080:8080 -> port mapping
# at the end - image name
docker run --name mywildfly -d -p 8080:8080 jboss/wildfly
```

### 3. Create a network and run detached container

```bash
# create netowrk `mynetwork`
docker network create mynetwork
# run container in that network
docker run --name mywildfly-net -d --net mynetwork \
-p 8080:8080 jboss/wildfly
```

### 4. Run a detached container mounting a local folder inside the container:

```bash
#
docker run --name mywildfly-volume -d \
-v myfolder/:/opt/jboss/wildfly/standalone/deployments/ \
-p 8080:8080 jboss/wildflyjboss/wildfly
```

### 5. Follow the logs of a specific container

```bash
docker logs -f <container-name-or-id>
# prints last 100 lines of the container
docker <container-name-or-id> logs --tail 100
```

### 6. List containers

```bash
docker ps # only active ones
docker ps -a # all
```

### 7. Stop a container

```bash
# stop the container
docker stop <container-name-or-id>
# stop container with timeout => 1s
docker stop -t1 <container-name-or-id>
```

### 8. Remove a container

```bash
# Remove a stopped container
$ docker rm [container-name|container-id]
# Force stop and remove a container
$ docker rm -f [container-name|container-id]
# Remove all containers
$ docker rm -f $(docker ps -aq)
# Remove all stopped containers
$ docker rm $(docker ps -q -f “status=exited”)

```

### 9. Execute process inside the container

```bash
# Execute and access bash inside a WildFly container
$ docker exec -it mywildfly bash

```

### 10. Restart the container

```bash
docker restart <container-name-or-id>
```

### 11. Display the running processes of the container

```bash
docker container top <container-name-or-id>
```

### 12. Display a live stream of container(s) resource usage statistics

```bash
docker container status <container-name-or-id>
```

### 13. Attach container execution to terminal session

```bash
docker attach <container-name-or-id>
```

### 14. Kill the container (not removing it)

```bash
docker kill <container-name-or-id>
```

### 15. Make short-term container (removes it after it is shut down)

```bash
docker run -it --name <container-name> --rm <image-name>
```

### 16. Pause container execution

```bash
docker pause <container-name-or-id>
```

### 17. Prune container

```bash
# with --all (removes all of them)
docker container prune
```

## Examples:

**TODO**

## 2. Image related commands

### 1. Build an image using a Dockerfile:

```bash
#Build an image
$ docker build -t [username/]<image-name>[:tag] <dockerfile-path>
	#Build an image called myimage using the Dockerfile in the same folder where the command was executed
$ docker build -t myimage:latest .
```

### 2. Check the history of the image

```bash
# Check the history of the jboss/wildfly image
$ docker history jboss/wildfly
	 # Check the history of an image
$ docker history [username/]<image-name>[:tag]
```

### 3. List the images

```bash
docker images
```

### 4. Remove the image from the local registry

```bash
docker rmi [username/]<image-name>[:tag]
```

### 5. Tag an image

```bash
# Creates an image called “myimage” with the tag “v1” for the image jboss/wildfly:latest
$ docker tag jboss/wildfly myimage:v1
# Creates a new image with the latest tag
$ docker tag <image-name> <new-image-name>
# Creates a new image specifying the “new tag” from an existing image and tag
$ docker tag <image-name>[:tag][username/] <new-image-name>.[:new-tag]
```

### 6. Exporting and importing an image to an external file

```bash
# Export the image to an external file
$ docker save -o <filename>.tar
# Import an image from an external file
$ docker load -i <filename>.tar
```

### 7. Push an image to a registry:

```bash
docker push [registry/][username/]<image-name>[:tag]
```

### 8. Pull (download) the image

```bash
docker pull <ime image>
```

### 9. Prune image (dangling images)

```bash
# --all ili -a (to clean all dangling images)
docker image prune
```

### 10. Search image

```bash
docker search <image-name>
```

# 3. Dockerfile

TODO

# 4. Docker compose

TODO
