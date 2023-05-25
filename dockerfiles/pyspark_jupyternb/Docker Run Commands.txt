#Create a docker image names pyspark with docker file present in current working directory
docker build -t pyspark .

#Run a docker image named pyspark & exposes container 8888 port to host's 8888 port
docker run -p 8888:8888 pyspark