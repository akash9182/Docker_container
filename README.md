## Project_1_docker
### Docker Link - https://cloud.docker.com/repository/docker/ranaas/hw3

### Steps to run my app using docker (follow any one of them)
- Using Docker 
```
docker pull ranaas/hw3:latest
docker run -d -p 8081:80 ranaas/hw3:latest

```
- Using googledrive
 [Download link](https://drive.google.com/file/d/1QEoxLVJLtvYxa9zFRJbGifxm9qdJ2dwT/view?usp=sharing)                 
 ```
 docker load -i cloud_project1.tar
 docker run -d -p 8081:80 ranaas/hw3:latest 
 ```

- I have combined HW2 REST API and HW3 WebApp and port it to a docker container.
* Creating Docker instance acts as a more portable and modular framework for hosting services.
* Docker helps for Isolation, Modularity, Scalability. It also increases the speed for deploying an application without having to worry about the overheads.

### Steps to install Docker:
- Set up the Repository 
```
 
 sudo apt-get update
 sudo apt-get install docker.io
 sudo usermod -a -G docker [username] (In my case it was ubuntu) 
 
```


### My Dockerfile looks like this (vim Dockerfile) :
```
FROM python:3.6

WORKDIR HW3

COPY ./requirements.txt /HW3/requirements.txt

RUN pip install -r requirements.txt

COPY . /HW3

RUN chmod +x startme.sh

CMD ["./startme.sh"]
```

### I Created a Makefile for the ease of running commands (vim Makefile) :
```
# builds docker file
docker-build:
        docker build -t ranaas/hw3:latest .
        
# pushes the docker file to dockerhub
docker-push:
        docker push ranaas/hw3:latest

# runs the docker image on my local machine
docker-run-dev:
        docker run -p 5000:80 ranaas/hw3:latest 

# runs the docker image on server
docker-run-prod:
        docker run -p 8081:80 ranaas/hw3:latest 

# view the content of the image
docker-run-it:
        docker run -ti ranaas/hw3:latest sh

```

### My startme.sh looks like this(vim startme.sh) :
```
#!/bin/bash

python3 app.py
```



