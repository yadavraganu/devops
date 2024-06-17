# Why Docker
- Docket makes it easy to run & install softwares without worrying about setup & dependencies
# What is docker
Docker is a platform or ecosystem around running & creating the containers  
__Image__ : Single file which have all the dependecies & config required to run the program  
__Container__ : Running instance of image called containers  
  
__Docker Client__ : Tool that is used to issue commands  
__Docker Server(Daemon)__ : Tool that is responsible for creating images ,running containers etc    

- Check docker version  
`docker version`
- Run a container  
`docker run hello-world`  
1. We ran command to run the container of hello-world image on docker CLI.
2. Docker server check in the local storage(image cache) if hello-world image is availble or not.
3. If it is not availabel docker server reaches out to dokcer hub (Repository of images).
4. It downloads iamge from docker hub & stores in image cache on local storage.
5. Run the image to create a container.
6. If we run same command again it will not go to docker hub.It can get from image cache.
- Run a command in container  
`docker run hello-world echo Hi New command` 
- List running container  
`docker ps`
- List all container created  
`docker ps --all`
- Create container  
`docker create`
- Start container  
`docker start`
# docker build
```
# Create image with Dockerfile present in current directory
docker build .

# Create image with name/tag assigned
docker build -t user/imagename:version .

# Create image with Dockerfile present in different directory
docker build -f ctx/Dockerfile
docker build -f dockerfiles/Dockerfile.debug -t myapp_debug .
docker build -f dockerfiles/Dockerfile.prod  -t myapp_prod .

# Other Options
--no-cache		Do not use cache when building the image
--rm                    Remove intermediate containers after a successful build
-q, --quiet		Suppress the build output and print image ID on success
```
# docker volume / mounts
Docker containers are immutable by nature. This means that restarting a container erases all your stored data in the container. But Docker provides volumes and bind mounts, which are two mechanisms for persisting data in your Docker container.  
-v or --volume allows you to mount local directories and files to your container. For example, you can start a MySQL database and mount the data directory to store the actual data in your mounted directory  
Binding a directory is a 2-way sync. Every file you change on the host is changed in the container, and every file that is changed in the container is changed on the host. So if you stop and start the database, you can mount the same directory, and your configuration and stored data will be available  

`docker run --name mysql-db -v $(pwd)/datadir:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:8.0.28-debian`

Instead of binding your local directory, you can use Docker volumes. A Docker volume is a directory somewhere in your Docker storage directory and can be mounted to one or many containers. They are fully managed and do not depend on certain operating system specifics.  
```
# create volume
docker volume create mysql-data

# run mysql container in the background
$ docker run --name mysql-db -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest

# stop mysql container
docker rm -f mysql-db

# remove volume
docker volume remove mysql-data
```

 It’s recommended to use them for persisting files that you don’t need to observe or change from your host system. This method is known to have better performance than local directory bindings.
 
