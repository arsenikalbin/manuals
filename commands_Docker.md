- **ARG** is only available during the build process, not after the image is built.  
is used to pass arguments to the Dockerfile from the docker-compose.yml file or from the command line.  
E.g. `docker build --build-arg BASE_IMAGE="nvidia_x86_64_humble_nv2" -t humble_realsense:latest .`  

--- Docker commmands ---

--- Buid image
docker build -f Dockerfile.aarch64.humble.nav2.realsense -t humble_realsense:latest --build-arg BASE_IMAGE="nvidia_x86_64_humble_nv2" ..

Rebuild docker image:
`docker build --no-cache -t humble_realsense:latest ..`

--- Run new terminal in the running container
docker exec -it <container-name/ID> bash

--- Run docker containers with GUI ---
xhost +local:root 
OR
xhost +

docker run -it --rm --privileged --network host --runtime=nvidia --gpus all --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" aarch64_humble_realsense:latest  
(--rm Automatically remove the container when it exits)  
(--gpus # flag when you start a container to access GPU resources. Specify how many GPUs to use (all - use all GPUs))  
(--privileged flag gives all capabilities to the container, and it also lifts all the limitations enforced by the device cgroup controller.   
(--volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" read-write mode (i.e. the container can write as well as read files on the host))  
In other words, the container can then do almost everything that the host can do)  

To capture docker build logs to a file
 `docker build -f Dockerfile.bfb_camera_d435i -t bfb_camera_d435i:latest ../.. 2>&1 | tee build.log`
 2>&1 redirects stderr to stdout, and then | tee build.log pipes stdout to tee, which writes it to build.log and also displays it on the screen.

--- end of block 'run docker containers wit GUI ---

--- Create and start containers
docker compose -f docker-compose_lenovo.yml up # Version2

docker-compose up
docker-compose up --build (Build images before starting containers.)

--- Start the stopped containers, can't create new ones
docker-compose start

--- Stop and remove containers, networks, images, and volumes
docker-compose down

--- List containers
docker-compose ps
docker ps -a

--- Inspect (containers, networks, images, volumes)
`docker inspect <container name>` - show container info (IP address, etc)
   docker container inspect 2186a1927d6a | grep compose 
`docker inspect <network name>` - show network info
`docker inspect <image name>` - show image info
`docker inspect <volume name>` - show volume info

--- end of block 'docker commmands ---