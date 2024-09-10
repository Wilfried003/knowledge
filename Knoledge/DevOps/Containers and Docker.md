
# 1. Installation de docker

 [[https://docs.docker.com/get-started/get-docker/| Cliquer ici]]  pour la doc officiel d'installation..

## a. Windows 

Il faut juste télécharger docker desktop et l'installer. Il fonctionnera également en ligne de commande.
![[Pasted image 20240823205634.png]]
## b. Linux
Suivre les instructions du site.

# 2. Introduction

## What is Docker

## Docker architecture

### a. Get Docker desktop and CLI

- Run your first docker
```copy
docker run -d -p 8080:80 docker/welcome-to-docker
```

Cette commande permet de lancer le container 'docker/welcome-to-docker'. Si elle n'existe pas en local, elle télécharge l'image docker avant de créer le container.
les options permettent :
 - -d : de lancer un arrière plan le conteneur, on aura pas les logs en vu.
 - -p : de faire un binding entre le port de l'application du container et le port sur lequel ma machine physique pourra accéder  pour lancer l'application 

### b. Develop with containers

Docker compose est souvent utilisé pour des projet nécessitant l'utilisation de volume ou plusieurs containers communiquant mutuellement.


* Run un projet en uploadant les modif en temps reel.
```compose
docker compose watch
```

We will learn how :
- Build and run an image as a container.
- Share images using Docker Hub.
- Deploy Docker applications using multiple containers with a database.
- Run applications using Docker Compose.

### Architecture Docker

Docker est essentiellement composé de 3 parties: 
![[Pasted image 20240826164906.png]]
- *Docker client*: il permet d'envoyer de requete en ligne de commande (ex: docker run) vers docker daemon via docker API
- *Docker Engine:* c'est le moteur de docker, il regroupe en son sein, docker daemon, qui ecoute et recoit le requete du client (docker fonctionne en client server), API docker, les images et les containers
- *Docker registry:* c'est la partie de stockage de docker (avec docker hub à l'interieur).
En installant Docker desktop, on installe par la meme occasion ses 3 parties. toutefois il est possible d'avoir que le *docker engine* sur un hote et le requete a partir d'un autre post sur lequel il aura *docker client*.

### Configuration REST API for docker

![[Pasted image 20240826170034.png]]

###  Build and run an image as a container.

Afin de travailler sur cette partie, nous utiliserons une application to-do existante. L'idée n'etant pas d'apprendre à coder mais d'utiliser les docker.

```clone
git clone https://github.com/docker/getting-started-app.git
```

On a récuperé un projet web, avec un server nodejs. Mais, nous n'avons pas de node sur notre machine. On va donc créer une image habritant node et pouvant deployer l'application.

Un moyen les plus courant de Builder une image est d'utilisé *Dockerfile*. 
*Dockerfile* est un fichier sans extention contenant une suite d'instruction pour créer une image Docker.
```Dockerfile
# syntax=docker/dockerfile:1
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```

1. On part d'une image deja existant de node *FROM* 
2. on se met dans notre environnement de travail *WORKDIR*
3. On copie de notre repertoire courant vers le repertoire de travail (\app) *COPY*
4.  qu'est ce qu'on lance pour la creation du conteneur, ici c'est un gestionnaire de dependance  *RUN*
5. Instruction qui est lancé au demarrage du conteneur *CMD*
6. Le port utiliser par le conteneur, il est a titre indicatif car la conf est deja dans le fichier du conf du serveur *EXPOSE*

Commande pour build l'app 
```Build
docker build -t getting-started .
```

	L'option *-t* permet de renommer l'image docker qui va etre créer 
Le *.* situe l'emplacement du Dockerfile.

Command pour lancer un conteneur.
```container
docker run -dp 127.0.0.1:3000:3000
```

1. l'option -d : lance en arriere plan
2. -p : faire du biding entre le port de la machine hote et le port du conteneur

### Share the application (Docker hub)

Pour partager l'avancer de ses images avec docker hub, il faut d'abord se connecter a docker hub.

```login
docker login -u YOUR-USER-NAME
```

```push
docker push USER-NAME/IMAGE-NAME
```

### Persist the BD

De base, tout container crée se cree avec son propre system de fichier, qui ne peuvent pas interragir avec d'autre container.

```
docker run -ti --name=nameContainer alpine /bin/ash
docker exec -ti containerName /bin/bash
```

Les volumes viennent remedier à cela. Avec les volumes il est possible de partager des systemes de fichiers. Il permet de connecter à un docker, un system de fichier connecter au systemm hote.


Il existe principalement deux types de volumes :
```
docker volume ls

docker volume create volumeName

docker run -d -v volumename:/containerVolumePath ubuntu

docker volume inspect nomVolume

docker run -ti --name c2 --rm -v volumeName:/path debian:latest bash
```

On ne peut monter un volume sur un conteneur qu'à sa création.

Lorsqu'on crée un volume, il est vide
Il est possible de créer un conteneur qui ce supprimera une fois fermée.

```
docker run -ti --name nameContainer --rm -v nameVolume:/path-to-volume debian:latest bash

exit
```

```
docker volume rm volumeName
```


Differents type de volumes :
1. Bind mount

en faisant un lien avec un repertoire fichier de notre hote et un repertoire du container
```bind
docker run -v/--volume /hote/path/vers:/dest/path debian:latest

docker run --name c1 --mount type=bind/volume/tmpfs, source=/source/path, target=/dest/path nginx/latest
```

il n'est pas manager par docker donc on ne retrouvera pas dans *docker volume ps*
2. Docker volume
On laisse ici docjer se charger de ou le volume sera crée sur notre hote, sauf qu'il sera vide
```dokerVolume
docker run -v my_volume:/data my_image
```

3. tmps mount
Un volume temporaire directement sur la RAM qui se detruit une fois le container supprimée

	pour certaine image, docker utilise pluseurs couche	
	Docker cree sa propre carte reseau
	0.0.0.0:8081 signifie a parti de n'importe quelle machine
	docker version

![[Pasted image 20240826130829.png]]

```attach
docker attach permet de s'attacher à un processus deja en cours (rappel toi par exemple de l'option *d qui execute en backgorund)
```

une chose importante dans l'utilisation de docker est qu'on crée un conteneur par service. un conteneur est cree pour moduler une application (micro service).
On veut une application web avec une base de données, on créera un conteneur pour la bdd et une autre pour lancer le serveur web. On pourra ensuite gerer les application multicontainer avec *compose.*

Ex : Lançons une application *Hello Word* le plus simple possible.
1. faire la page html
```index.html
<p>Hello Wold</p>
```
2. Le serveur qui lancera la page
```Dockerfile
FROM nginx
COPY index /path/to/nginx/www -> /usr/share/nginx/html

EXPOSE 8080
```

Ex: Creer un projet jar avec docker


### Networking in docker

* Bridge : Par defaut: docker run nginx -> les conteneurs ont une addresse ip distinct mais tous dans le meme reseaux, on peut utiliser le meme port 
* Host : docker run --network=host nginx -> les conteneurs utilise l'ip de la machine , on ne peut pas utiliseer le meme port
* none: docker run --network = none nginx -> impossible de le contacter avec un autre conteneur

 - Creer un network
 - ajouter un container
 - un container peut appatenir a pplusieurs network (il aura plusierus interface resaue)
 - communiquer en eux
 - laner un contenur avec un network directement

### Docker Layered architecture

### Docker compose

Il est utiliser pour gerer des applications multiontainer
* un fichier docker-compose.yml est utilisé pour configurer les liens entre les conteneurs
![[Pasted image 20240826232312.png]]

```
docker compose up
```
Il recherche le fichier *docker-compose.yml* et fais les *run* de chaque service.

-- links

![[Pasted image 20240826234052.png]]

![[Pasted image 20240826234125.png]]

Dans docker compose 1 on specifie avec links les conteneurs qui communiquent entre eux mais pas dans la version 2. ils sont tous relié entre eux.

compose se charge de faire les *run*

![[Pasted image 20240826235318.png]]
![[Pasted image 20240826235409.png]]


Pour distinger les reseaux
![[Pasted image 20240826235716.png]]


### Kubernetes
- surveille la santé des conteneurs et du docker engine
utiliser kubernitest avec ggogle cloud
