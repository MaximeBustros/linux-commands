# Docker
## Docker run
-d: detached mode

-p: port binding (\<local-port>:\<remoteport>)
* Example: docker run -p 80:8000
-v: bind volume.  
* Named volumes: Docker manages where to store the volume
   * To create volume: docker volume create \<volume-name>
   * To attach volume: docker -v \<volume-name>:\<docker-path> 
   * Note: If we attach a volume without creating the volume first then it is created automatically
* Bind mounts: Mounts a local path to docker path
   * To attach volume: docker -v \<local-path>:\<docker-path>

-w: set working directory of docker
* Example:
    * docker run -d -w /usr ubuntu tail -f /dev/null: Runs a docker container in the background
    * docker exec \<container-id> ls: Shows you that your root directory / is actually /etc/

--network: to attach a network to docker container
* Example: 
   * docker run -d --network \<network-name>

--network-alias: allows you to set a hostname to your container to resolve ip
* Example:
    * docker run -d --network \<network-name> --network-alias \<my-network>

# Docker volume
allows you to create a named volume

To create a volume:
* docker volume create \<volume-name>

# Docker network
Allows you to create a network

To create a network:
* docker network create \<network-name>


## Interesting images for debugging
* nicolaka/netshoot allows you to lookup ip addresses on a network:
    * To Run: docker run -it --network \<network-name> nicolaka/netshoot
    * To use: dig \<hostname>


# Docker-compose
## Docker-compose up
* To use: docker-compose up

-d: Allows you to run in the background

## Docker-compose logs
-f: see the logs from each of the services interleaved into a single stream

## Docker-compose down
Take down all services

# Image building best practices
## Security scanning
Scan image with docker scan to check for vulnerabilities
* How to use: docker scan /<image-name>

## Image layering
Used to check what makes up an image
* How to use: docker image history /<image-name>
* --no-trunc: To get full output

## Layer caching
Once a layer changes, all downstream layers have to be recreated as well

To avoid rebuilding it can be a good thing to insert dependencies at the start of the file to avoid rebuilding them everytime


## Docker-ignore
.dockerignore: is a file that should be at the same level as the dockerfile

It allows an easy to way to selectively copy only image relevant files

For example: We could add node_modules in the case of a node project as they will not be copied during the copy of the app.

## Multi-stage builds
Advantages of multi-stage builds:
* Separate build-time dependencies from runtime dependencies
* Reduce overall image size by shipping only what your app needs to run

