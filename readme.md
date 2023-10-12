# Docker Workshop

## 1 - About virtualization?

the `Virtualization` and `containerization` are two seperate methods and technologies even if they look the same as shoween in the illustrrations.

![virtualization illustartion](https://www.researchgate.net/publication/269636339/figure/fig1/AS:295113902313473@1447372045341/illustration-of-the-concept-of-Virtualization-7.png)

![containerization illusatrtion](https://media.geeksforgeeks.org/wp-content/uploads/20190915151739/docker_flowchart-1024x640.png)

for more infomation and understanding please check [this video](https://www.youtube.com/watch?v=0qotVMX-J5s)

Docker can be used with two Method
 - Docker cli
 - Docker desktop

## 2 - Docker CLI

***docker is required for this chapter***

### 1 - pull/run image

let's take `postgreSQL` as an example in this chapter

first of all lets pull the official docker image from [DockerHUB](https://hub.docker.com/)

```docker pull postgres:latest``` ||
`docker pull <image-name>:tag`

after the image is pulled we should run it using ```docker run -d -p 5432:5432 --name postgres postgres``` || ```docker run -d -p 5432:5432 --name <container-name> <image-name>```.

*BINGO*, the container is created

### 2 - access to the container

let suppose you want to get the access or go through the container folder, for that you should use: ```docker exec -it postgres bash``` || ```docker exec -it <container-name> bash``` .

in general, you can use whatever service you want, in condition that the service is alive in the conatiner.for example let's suppose that you want to execute `psql` service, we can use the following command: ```docker exec -it postgres psql -U aymane myDB```  || ```docker exec -it postgres psql -U <db-user> <db-name>``` .

### 3 - cleaning

for cleaning in docker we should pay attention to three terms:
 - volumes
 - containers
 - images

so when we talk about cleaning/removing we should specify wish of those three should be in consideration.

 #### a - volumes

 volumes are a storage for conatiner. each container have a specific volumes that holds the data of the container(files, db data...), for that you can use ```docker volume prune``` or ```docker volume rm <volume-name1> <volume-name2>...```.

 you can use ```docker volumes help``` for more commands.

 #### b - container

 to remove a container is like the previous step you going to use this command ```docker container rm <container-name|container-id>1 <container-name|container-id>2``` .

 you can use ```docker conatiner help``` for more commands.

  #### c - images

 to remove an image you are going to use the following command ```docker image rm <image-id1> <image-id2>``` .

 you can use ```docker image help``` for more commands.

## 4 - docker desktop

for a quick overview i ghighly recommnd the following [video](https://www.youtube.com/watch?v=hwoWBdNilVI).

## 5 - Dockerfile

[Dockerfile](https://docs.docker.com/engine/reference/builder/) is a manifest file in `YAML` that contain the necessary steps to build/configuer a container for your work.

in general the Dockerfile have a syntax as the following:

```
FROM image:tag

WORKDIR directory

ENV var=value
.
.
.

COPY local_destination container_destination
.
.
.

RUN bash_command
.
.
.

EXEC ['final', 'command', 'to', 'be', 'executed']
```

- `FORM` used to pull the hosted image in docker hub with it's tag.
- `WORKDIR`: specifiy the directory that container the files for our project
- `ENV`: define a environement variable 
- `COPY`: copy file, folder from your local disque to the conatiner volume
- `RUN`: used to run non-blocking bash command
- `EXEC`: in general is used to execute a command when the container is started, it only accept one command.

we can use/execute all the previous command to run, pull our conatiner using Dockerfile.

 let's take the following [Dockerfile](./Dockerfile) as example.

to run this file you qre doing the following

#### 1 - build image from the Dockerfile

```
docker build -t postgres .
```
`-t` is used to give a tag/name for the image in build

#### 2 - run the container

the next step after building the container, is to run it for that you are going to run the following:
```
docker run -d --name postgres -p 5432:5432 postgres
```

and that's it the container is alive!

## 7 - Container lifecycle

![lifecycle](https://media.licdn.com/dms/image/D4D12AQFCRiHIoz4arw/article-cover_image-shrink_423_752/0/1682912967953?e=1702512000&v=beta&t=XWVGknTGrKDRTZs_AwvjRHG1ztc7zD_ekzOBsq-ZPA4)

the lifecycle of a container can be divided into 3 main parts:
 - start
 - pause
 - restart
 - delete

 #### 1 - start

 after we run the conatiner for the first time the container is started by default.but sometimes when ew restart or server/personal laptop... the conatiner is stopped and restarted we use ```docker start <container-name>```

  #### 2 - pause

  docker give us the possiblity to pause/unpause our container using

  ```docker pause|unpause <container-name>```

  ##### 3 - restart

  we can also restart our container, in some cases restarting your conatiner is required when one conatiner depends on another and for that to keep everything sync we should restarted. ```docker restart <container-name>``
  
  #### 4 - delete
  you can delete your container by typing ```docker start <conatiner-name>```