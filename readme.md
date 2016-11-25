![Docker logo](https://raw.githubusercontent.com/theodorosploumis/drupalcamp2016/gh-pages/img/docker_logo.png)

## Using Docker with Drupal - Introduction

#### [DrupalCamp 2016](http://www.drupal-camp.gr), 1-3 July 2016

###### [TheodorosPloumis.com](http://www.theodorosploumis.com/en) / [@theoploumis](http://twitter.com/theoploumis)
________________________

###### Get them: [online presentation](http://theodorosploumis.github.io/drupalcamp2016/) / [source code](https://github.com/theodorosploumis/drupalcamp2016) / [docker image](https://hub.docker.com/r/tplcom/drupalcamp2016/)

###### Under [Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/) license.

---

### What is Docker

> Docker is an open platform for developing, shipping, and running applications.

---

### Docker vs VMs

![Docker vs traditional Virtualization](https://raw.githubusercontent.com/theodorosploumis/drupalcamp2016/gh-pages/img/vm_vs_containers.png)

---

### From Monolithic apps

![Monolithic Architecture](https://raw.githubusercontent.com/theodorosploumis/drupalcamp2016/gh-pages/img/monolithic.png)

---

### To Containerized apps

![Containerized Architecture](https://raw.githubusercontent.com/theodorosploumis/drupalcamp2016/gh-pages/img/containerized.png)

---

### Docker History

 - Solomon Hykes ([@solomonstre](https://twitter.com/solomonstre))
 - dotCloud (now Docker Inc)
 - March 2013
 - Apache 2.0 license
 - 37k stars on [Github](https://github.com/docker/docker)
 - 270k public repositories on docker hub

---

### Docker Benefits

 - Fast (deployment, migration, restarts)
 - Secure
 - Lightweight (save disk & CPU)
 - Open Source
 - Portable software
 - Microservices and integrations (APIs)
 - Simplify DevOps
 - Version control capabilities

---

### Common Docker usages

 - Scaling apps
 - Development collaboration
 - Infrastructure configuration
 - Sandbox (develop, test, debug, educate etc)
 - Local development
 - Continuous Integration & Deployment
 - Multi-tier applications
 - PaaS, SaaS

###### See the [survey results for 2016](https://www.docker.com/survey-2016)

---

### Technology stack

 - Linux [x86-64](https://www.wikiwand.com/en/X86-64) & Windows (Hyper-V)
 - [Go](https://golang.org/) language
 - [Client - Server](https://www.wikiwand.com/en/Client%E2%80%93server_model) (deamon) architecture
 - Union file systems ([UnionFS](https://www.wikiwand.com/en/UnionFS): AUFS, btrfs, vfs etc)
 - [Namespaces](https://en.wikipedia.org/wiki/Cgroups#NAMESPACE-ISOLATION) (pid, net, ipc, mnt, uts)
 - Control Groups ([cgroups](https://www.wikiwand.com/en/Cgroups))
 - Container format ([libcontainer](https://github.com/opencontainers/runc/tree/master/libcontainer "Libcontainer provides a native Go implementation for creating containers with namespaces, cgroups, capabilities, and filesystem access controls. It allows you to manage the lifecycle of the container performing additional operations after the container is created."))

###### See more at [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### The Docker architecture

![Docker architecture](https://docs.docker.com/engine/article-img/architecture.svg)
###### See more at [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### Docker components

 - (Docker) client
 - daemon
 - engine
 - machine
 - compose
 - swarm
 - registry

---

### Docker client

It is the primary user interface to Docker. It accepts commands from the user
and communicates back and forth with a Docker daemon.

---

### Docker daemon

It runs on a host machine. The user does not directly interact with the daemon,
but instead through the Docker client with the RESTful api or sockets.

---

### Docker engine

A Client with a Daemon as also as the docker-compose tool. Usually referred simply as "docker".

![Docker engine logo](https://raw.githubusercontent.com/theodorosploumis/docker-java/master/img/docker_logo_simple.png)

---

### Docker machine

A tool which makes it really easy to create Docker hosts on your computer,
on cloud providers and inside your own data center.
It creates servers, installs Docker on them, then configures the Docker client to talk to them.

![Docker machine logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_machine.png)

---

### Docker compose

A tool for defining and running complex applications with Docker
(eg a multi-container application) with a single file.

![Docker compose logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_compose.png)

---

### Docker swarm

A native clustering tool for Docker. Swarm pools together several Docker
hosts and exposes them as a single virtual Docker host. It scale up to multiple hosts.

![Docker swarm logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_swarm.png)

---

### Docker distribution

A (hosted) service containing repositories of images which responds to the Registry API.

![Docker distribution logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_distribution.png)

---

### The Docker Components diagram

![Docker components](https://raw.githubusercontent.com/theodorosploumis/docker-java/master/img/docker-components.png)

---

### Steps of a Docker workflow

```
docker run -i -t ubuntu:15.04 /bin/bash
```

 - Pulls the ubuntu:15.04 [image](https://docs.docker.com/engine/userguide/containers/dockerimages/ "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot.") from the [registry](https://docs.docker.com/registry/ "The central place where all publicly published images live. You can search it, upload your images there and when you pull a docker image, it comes the repository/hub.")
 - Creates a new [container](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/ "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides.")
 - Allocates a filesystem and mounts a read-write [layer](https://docs.docker.com/engine/reference/glossary/#filesystem "A set of read-only files to provision the system. Think of a layer as a read only snapshot of the filesystem.")
 - Allocates a [network/bridge interface](https://www.wikiwand.com/en/Bridging_%28networking%29)
 - Sets up an [IP address](https://www.wikiwand.com/en/IP_address "An Internet Protocol address (IP address) is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication.")
 - Executes a process that you specify (``` /bin/bash ```)
 - Captures and provides application output

Screencast: [Steps of a Docker workflow](https://asciinema.org/a/1yqyy1uu1taxciqf4136sy3ld).

---

### The docker image

![ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/image-layers.jpg "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot. Each Docker image references a list of read-only layers that represent filesystem differences. Layers are stacked on top of each other to form a base for a container’s root filesystem.")

---

### The docker container

![container using ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/container-layers.jpg "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides. For each containers there is a new, thin, writable layer - container layer - on top of the underlying stack (image).")

---

### The Dockerfile

> A Dockerfile is a text document that contains all the commands a user could call on the command line to create an image.

 - [Dockerfile with inline comments](https://github.com/theodorosploumis/docker-presentation/blob/gh-pages/examples/dockerfile/Dockerfile) just for education
 - [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) on docker docs
 - Public Dockerfiles ([wildfy](https://github.com/jboss-dockerfiles/wildfly/blob/master/Dockerfile), [Spring Boot](https://github.com/Bankmonitor/docker/blob/master/Dockerfile), [openjdk 9](https://github.com/docker-library/openjdk/blob/master/9-jre/Dockerfile))

---

### Common Docker Commands

```
// General info
man docker // man docker run
docker help // docker help run
docker info
docker version
docker network ls

// Images
docker images // docker [IMAGE_NAME]
docker pull [IMAGE] // docker push [IMAGE]

// Containers
docker run
docker ps // docker ps -a, docker ps -l
docker stop/start/restart [CONTAINER]
docker stats [CONTAINER]
docker top [CONTAINER]
docker port [CONTAINER]
docker inspect [CONTAINER]
docker inspect -f "{{ .State.StartedAt }}" [CONTAINER]
docker rm [CONTAINER]

```
Screencast: [Common Docker commands](https://asciinema.org/a/3hczjxzuvih674htyis6o8q6t)

----

### Docker examples

- Terminal inside a container
- [Linked](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/) containers
- Docker [Volume](https://docs.docker.com/engine/userguide/containers/dockervolumes/)
- Using [docker-compose](https://docs.docker.com/compose/)
- Advanced usage of docker-compose

---

### Example: SSH into a container

```
docker pull ubuntu
docker run -it --name ubuntu_example ubuntu /bin/bash
```
Screencast: [SSH into a container](https://asciinema.org/a/0z4bu6ub4l3z6n3t6b0d5e35g)

---

### Example: Docker link containers

Let's create a [Drupal app](https://hub.docker.com/_/drupal/) (apache, php, mysql, drupal)

```
cd ~/Docker-presentation
mkdir drupal-link-example
cd drupal-link-example

docker pull drupal:8.2.3-apache
docker pull mysql:8

// Start a container for mysql
docker run --name mysql_example \
           -e MYSQL_ROOT_PASSWORD=root \
           -e MYSQL_DATABASE=drupal \
           -e MYSQL_USER=drupal \
           -e MYSQL_PASSWORD=drupal \
           -d mysql:8

// Start a Drupal container and link it with mysql
// Usage: --link [name or id]:alias
docker run -d --name drupal_example \
           -p 8280:80 \
           --link mysql_example:mysql \
           drupal:8.2.3-apache

// Open http://localhost:8280 to continue with the installation
// On the UI for the db host use: mysql

// There is a proper linking
docker inspect -f "{{ .HostConfig.Links }}" drupal_example
```
Screencast: [Docker: Drupal and MySQL containers linked](https://asciinema.org/a/1bp6bb5tbq0hwuwgyck8ufo8j)

---

### Example: Docker volume

Let's mount local files to a docker container

```
cd ~/drupalcamp2016
drush dl drupal-8.1.2
cd ~/drupalcamp2016/drupal-8.1.2

// Start a container for mysql
docker run --name mysql_container \
           -e MYSQL_ROOT_PASSWORD=root \
           -e MYSQL_DATABASE=drupal \
           -e MYSQL_USER=drupal \
           -e MYSQL_PASSWORD=drupal \
           -d mysql:5.5

// Start drupal container with volume
// Folder "modules" locally is mounted to the container
docker run -d --name drupal_with_mysql_volumed \
           -p 8290:80 \
           --link mysql_container:mysql \
           -v $(pwd)/modules:/var/www/html/modules \
           drupal:8.1.2-apache

drush dl devel
// Devel module is available on the container

```

---

### Example: Using Docker Compose

Let's create a Drupal app using [docker-compose.yml](https://github.com/theodorosploumis/drupalcamp2016/blob/gh-pages/examples/docker-compose/simple/docker-compose.yml)

```
git clone git@github.com:theodorosploumis/drupalcamp2016.git \
          ~/drupalcamp2016/presentation
cd ~/drupalcamp2016/presentation/examples/docker-compose/simple

// Run docker-compose using the docker-compose.yml
docker-compose up -d
```

---

### Example: More advanced docker-compose

[Drupal + friends](https://github.com/theodorosploumis/drupal-docker) together.

```
cd ~/drupalcamp2016
git clone git@github.com:theodorosploumis/drupal-docker.git
cd ~/drupalcamp2016/drupal-docker

docker-compose up -d

// Open http://localhost:8081 (web)
// Open http://localhost:8090 (phpmyadmin)

// Prepare Drupal for installation
docker exec drupal_8081 bash /scripts/prepare-install.sh

// Install with Drush
docker exec drupal_8081 /drush/drush \
    site-install -y standard \
    --site-name="Drupal 8 with Docker - Drush" \
    --db-url=mysql://drupal:drupal@mysql/drupal \
    --site-mail=admin@example.com \
    --account-name=admin \
    --account-pass=admin \
    --account-mail=admin@example.com

```

---

### Docker tips

There are known best practices (see a list at [examples/tips](https://github.com/theodorosploumis/drupal-presentation/tree/gh-pages/examples/tips))

- Optimize containers (see [imagelayers.io](https://imagelayers.io/?images=drupal:8.1.0-fpm))
- Create your own, tiny base images
- Containers are not Virtual Machines
- Full stack Images VS 1 process per Container
- Use files/scripts to setup container
- Prefer using docker-compose
- Production needs orchestration tools

---

### The Docker war

| Type | Software |
|:----:|----------|
| Cluster &<br>Orchestrate | [Swarm](https://docs.docker.com/swarm/), [Kubernetes](http://kubernetes.io/), [Rancher](http://rancher.com/), [Marathon](https://mesosphere.github.io/marathon/), [MaestroNG](https://github.com/signalfx/maestro-ng), [decking](http://decking.io/), [shipyard](http://shipyard-project.com/) |
| Registry | [Portus](http://port.us.org/), [Distribution](https://github.com/docker/distribution), [hub.docker.com](http://hub.docker.com), [quay.io](https://quay.io), [G. Container Registry](https://cloud.google.com/tools/container-registry/), [projectatomic.io](http://www.projectatomic.io/) |
| PaaS | [Rancher](http://rancher.com/), [Tsuru](https://tsuru.io/), [dokku](https://github.com/dokku/dokku), [flynn](https://flynn.io/),  [Octohost](http://octohost.io/), [DEIS](http://deis.io/) |

---

### Instead of Resources

 - [docs.docker.com](https://docs.docker.com/)
 - Books: [Docker in Practice](https://www.manning.com/books/docker-in-practice), [The Docker Book](http://www.dockerbook.com/)
 - Tools: [terra](http://terra.readthedocs.io/) / [drude](https://github.com/blinkreaction/drude) / [dropdock](http://dropdock.io/), [kalabox](https://github.com/kalabox/kalabox) / [bowline](https://github.com/davenuman/bowline) / [webfactory](https://github.com/Boran/webfact) / [DockerDrupal](https://www.4alldigital.io/docker-drupal) / [drocker](https://github.com/gabesullice/drocker)
 - Community: [Dockerized Drupal](https://dockerizedrupal.com) / [D.O. Docker group](https://groups.drupal.org/docker) / [D.O. drupalci_testbot](https://www.drupal.org/project/drupalci_testbot)

---

### Questions?

![Drupal over Docker!](https://raw.githubusercontent.com/theodorosploumis/drupalcamp2016/gh-pages/img/dcamp_docker.png)

$this->send('[feedback](https://goo.gl/xa3moy)');
______________

###### Tools used: [oh my zsh](http://ohmyz.sh/) / [reveal.js](https://github.com/hakimel/reveal.js) / [Simple Docker UI for Chrome](https://github.com/felixgborrego/docker-ui-chrome-app) / [docker compose 1.9.0](https://github.com/docker/compose/releases/tag/1.9.0) / [docker 1.12.3](https://github.com/docker/docker/releases/tag/v1.12.3)
