![moby2.png](https://bitbucket.org/repo/adXy48/images/3814577896-moby2.png)
# Guide rapide de démarrage pour ce projet
Nous rappelons que Docker est un logiciel libre qui automatise le déploiement d'applications dans des conteneurs logiciels. C'est un outil qui peut empaqueter une application et ses dépendances dans un conteneur isolé, qui pourra être exécuté sur n'importe quel serveur Linux. Ceci permet d'étendre la flexibilité et la portabilité d’exécution d'une application, que ce soit sur la machine locale, un cloud privé ou public, une machine nue, etc.

Docker étend le format de conteneur Linux standard, LXC, avec une API de haut niveau fournissant une solution de virtualisation qui exécute les processus de façon isolée. Docker utilise LXC, cgroups, et le noyau Linux lui-même. 

Disons que Docker est une "sorte de machine virtuelle", mais Contrairement aux machines virtuelles traditionnelles, un conteneur Docker n'inclut pas de système d'exploitation, elle s'appuie sur les fonctionnalités du système d’exploitation fournies par l'infrastructure sous-jacente.


## Installer docker
Docker peut être installé sur Linux ou windows ou Mac (Architectures 64 bits et ARM seulement supportées).
Détails de l'installation sur : [Get Docker](https://www.docker.com/products/overview).
Dans le cas d'une Raspberry pi fonctionnant sous Raspbian l'installation se fait juste par la commande :

```
#!python

curl -sSL get.docker.com | sh
```
## Vérifier l'installation
On peut exécuter l'image officielle HELLO WOLD pour vérifier l'installation. La commande suivante devrait donner la sortie suivante si tout fonctionne correctement.

```
#!shell

 $ docker run hello-world
 Unable to find image 'hello-world:latest' locally
 latest: Pulling from library/hello-world
 535020c3e8ad: Pull complete
 af340544ed62: Pull complete
 Digest: sha256:a68868bfe696c00866942e8f5ca39e3e31b79c1e50feaee4ce5e28df2f051d5c
 Status: Downloaded newer image for hello-world:latest

 Hello from Docker.
 This message shows that your installation appears to be working correctly.

 To generate this message, Docker took the following steps:
 1. The Docker Engine CLI client contacted the Docker Engine daemon.
 2. The Docker Engine daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker Engine daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker Engine daemon streamed that output to the Docker Engine CLI client, which sent it
    to your terminal.

 To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

 Share images, automate workflows, and more with a free Docker Hub account:
 https://hub.docker.com

 For more examples and ideas, visit:
 https://docs.docker.com/userguide/
```


## Conteneurs et images
La commande suivante permet d'**afficher** tous les conteneurs présents sur le sytsème.

```
#!shell

docker ps -a

 CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
 592376ff3eb8        hello-world         "/hello"            25 seconds ago      Exited (0) 24 seconds ago                       prickly_wozniak
```

**Explication de la commande docker run hello-wolrd**

![container_explainer.png](https://bitbucket.org/repo/adXy48/images/3030846265-container_explainer.png)

**Lister les conteneurs en cours d'exécution**
```
#!shell

docker ps
```

**Arrêter un conteneur**
```
#!shell

docker stop <container id>
```

**Arrêter tous les conteneurs**
```
#!shell

docker stop $(docker ps -a -q)
```

**Effacer un conteneur**
```
#!shell

docker rm <container id>
```

**Effacer tous les conteneurs**
```
#!shell

docker rm $(docker ps -a -q)
```

**Lister toutes les images**
```
#!shell

docker images
```

**Effacer une image**
```
#!shell

docker rmi <image id>
```

**Effacer toutes les images**
```
#!shell

docker rmi $(docker images -q)
```

## Construire une image docker
Dans le cadre de ce projet, nous aurons besoins de contruire nos propres images docker, cette section illustres les étapes.

### Ecrire un Dockerfile
C'est un fichier qui va servir à dire à docker comment construire l'image.

**Créer un fichier DockerFile dans le dossier mydockerbuild**
```
#!shell

$ mkdir mydockerbuild
$ cd mydockerbuild
$ nano Dockerfile
```

**Ajouter l'image de base, ici whalesay** 
```
#!shell

FROM docker/whalesay:latest
```
** Installer le programme fortunes comme sous ubuntu avec la command RUN**
```
#!shell

RUN apt-get -y update && apt-get install -y fortunes
```

**Commande à exécuter quand l'environnement sera prêt**
```
#!shell

CMD /usr/games/fortune -a | cowsay
```

Le Dockerfile devrait ressembler à ceci

```
#!shell

FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
CMD /usr/games/fortune -a | cowsay
```

### Construire l'image docker



# Documentation complète sur docker

## Références
* [Site](https://www.docker.com/) officiel
* [Docker Hub](https://hub.docker.com/)
* [Docker Labs](https://github.com/docker/labs)
* [4-day Docker and Kubernetes Training](http://blog.christianposta.com/kubernetes/3-day-docker-and-kubernetes-training/)

### Avancé
* [Docker Cleanup Scripts Comparison](https://www.brianchristner.io/docker-cleanup-script-comparison/)
* [Docker Image Reduction Techniques and Tools](http://chrisstump.online/2016/02/23/docker-image-reduction-techniques/)
* [10 Practical Docker Tips for Day to Day Docker usage](http://www.smartjava.org/content/10-practical-docker-tips-day-day-docker-usage)

### GUI
* [Portainer](http://portainer.io/)
* [DockerUI](https://github.com/kevana/ui-for-docker)

### Docker et Raspberry Pi
* [Get Started with Docker 1.12 on Raspberry Pi](http://blog.alexellis.io/getting-started-with-docker-on-raspberry-pi/)
* [5 things about Docker on Raspberry Pi](http://blog.alexellis.io/5-things-docker-rpi/)