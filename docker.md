# Docker
## Docker run parameters
-d: detached mode

-p: port binding (\<local-port>:\<remoteport>)
* Example: docker run -p 80:8000
-v: bind volume.  
* Named volumes: Docker manages where to store the volume
   * To create volume: docker volume create \<volume-name>
   * To attach volume: docker -v \<volume-name>:\<docker-path> 
* Bind mounts: Mounts a local path to docker path
   * To attach volume: docker -v \<local-path>:\<docker-path>

-w: set working directory of docker
* Example:
    * docker run -d -w /usr ubuntu tail -f /dev/null: Runs a docker container in the background
    * docker exec \<container-id> ls: Shows you that your root directory / is actually /etc/