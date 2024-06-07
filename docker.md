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
