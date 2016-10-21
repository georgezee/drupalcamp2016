![Docker logo](https://raw.githubusercontent.com/theodorosploumis/drupalcamp2016/gh-pages/img/docker_logo.png)

## Using Docker with Drupal - Introduction

#### [DrupalCamp Cape Town](http://capetown2016.drupalcamp.co.za), 21 October 2016

###### George Ziady / george@springfisher.com
###### ---
###### credit to:
###### [TheodorosPloumis.com](http://www.theodorosploumis.com/en) / [@theoploumis](http://twitter.com/theoploumis)
###### [DrupalCamp Greece 2016](http://www.drupal-camp.gr), 1-3 July 2016
________________________

###### Get them: [online presentation](http://theodorosploumis.github.io/drupalcamp2016/) / [source code](https://github.com/theodorosploumis/drupalcamp2016) / [docker image](https://hub.docker.com/r/tplcom/drupalcamp2016/)

###### Under [Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/) license.

---

### What is Docker

> Docker is an open platform that automates the deployment of applications in software containers.

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

### About Docker project

 - [Solomon Hykes](https://twitter.com/solomonstre)
 - dotCloud (now Docker Inc)
 - March 2013
 - 36k stars on [Github](https://github.com/docker/docker/)
 - 450k public repositories on [hub.docker.com](https://hub.docker.com)

---

### Docker Benefits

 - Fast
 - Lightweight
 - Open Source
 - Portable
 - Microservices and integrations (APIs)
 - Extensible
 - Version control

---

### Common Docker usages

 - Sandbox environment (develop, test, debug, educate)
 - Continuous Integration & Deployment
 - Development collaboration
 - Prototyping
 - Infrastructure configuration
 - Multi-tier applications
 - Scaling apps
 - PaaS, SaaS

###### See the [survey results for 2016](https://www.docker.com/survey-2016)

---

### Technology behind Docker

 - Linux [x86-64](https://www.wikiwand.com/en/X86-64)
 - [Go](https://golang.org/) language
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

### Steps of a Docker workflow

```
docker run -i -t ubuntu:15.04 uname -a
```

 - Pulls the ubuntu:15.04 [image](https://docs.docker.com/engine/userguide/containers/dockerimages/ "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot.") from the [registry](https://docs.docker.com/registry/ "The central place where all publicly published images live. You can search it, upload your images there and when you pull a docker image, it comes the repository/hub.")
 - Creates a new [container](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/ "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides.")
 - Allocates a filesystem and mounts a read-write [layer](https://docs.docker.com/engine/reference/glossary/#filesystem "A set of read-only files to provision the system. Think of a layer as a read only snapshot of the filesystem.")
 - Allocates a [network/bridge interface](https://www.wikiwand.com/en/Bridging_%28networking%29 "")
 - Sets up an [IP address](https://www.wikiwand.com/en/IP_address "An Internet Protocol address (IP address) is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication")
 - Executes a process that you specify (```uname -a```)
 - Captures and provides application output

---

### The docker image

![ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/image-layers.jpg "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot. Each Docker image references a list of read-only layers that represent filesystem differences. Layers are stacked on top of each other to form a base for a container’s root filesystem.")

---

### The docker container

![container using ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/container-layers.jpg "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides. For each containers there is a new, thin, writable layer - container layer - on top of the underlying stack (image).")

---

### Explore Docker commands

```
// General info
man docker // man docker-run
docker help // docker help run
docker info
docker version

// Images
docker images // docker [IMAGE_NAME]
docker pull [IMAGE] // docker push [IMAGE]

// Containers
docker run
docker ps // docker ps -a
docker stop/start/restart [CONTAINER]
docker stats [CONTAINER]
docker top [CONTAINER]
docker inspect [CONTAINER]
docker inspect -f "{{ .State.StartedAt }}" [CONTAINER]
docker rm [CONTAINER]

```

---

### The Dockerfile

> A text document that contains all the commands a user could call on the command line to create an image.

 - [Dockerfile with inline comments](https://github.com/theodorosploumis/drupalcamp2016/blob/gh-pages/examples/dockerfile/Dockerfile) just for education
 - Drupal* Dockerfiles ([Drupal](https://github.com/docker-library/drupal/blob/master/8.1/fpm/Dockerfile), [drush/drush](https://github.com/RobLoach/drush-docker/blob/master/8/Dockerfile), [dropdog/docker](https://hub.docker.com/r/dropdog/docker/~/dockerfile/), [Boran/docker-drupal](https://github.com/Boran/docker-drupal/blob/master/Dockerfile), [ricardoamaro/docker-drupal](https://github.com/ricardoamaro/docker-drupal/blob/master/Dockerfile))

---

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

---

### Example: Docker link containers

Let's create a [Drupal app](https://hub.docker.com/_/drupal/) (apache, php, mysql, drupal)

```
docker pull drupal:8.2.1-apache
docker pull mysql:5.6

// Start a container for mysql
docker run --name mysql_container \
           -e MYSQL_ROOT_PASSWORD=root \
           -e MYSQL_DATABASE=drupal \
           -e MYSQL_USER=drupal \
           -e MYSQL_PASSWORD=drupal \
           -d mysql:5.6

// Start a Drupal container and link it with mysql
// Usage: --link [name or id]:alias
docker run -d --name drupal_with_mysql \
           -p 8280:80 \
           --link mysql_container:mysql \
           drupal:8.2.1-apache

// Open http://localhost:8280 to continue with the installation
// On the db host use: mysql

// There is a proper linking
docker inspect -f "{{ .HostConfig.Links }}" drupal_with_mysql
```

---

### Example: Docker volume

Let's mount local files to a docker container

```
cd ~/drupalcamp2016
drush dl drupal-8.2.1
cd ~/drupalcamp2016/drupal-8.2.1

// Start a container for mysql
docker run --name mysql_container \
           -e MYSQL_ROOT_PASSWORD=root \
           -e MYSQL_DATABASE=drupal \
           -e MYSQL_USER=drupal \
           -e MYSQL_PASSWORD=drupal \
           -d mysql:5.6

// Start drupal container with volume
// Folder "modules" locally is mounted to the container
docker run -d --name drupal_with_mysql_volumed \
           -p 8290:80 \
           --link mysql_container:mysql \
           -v $(pwd)/modules:/var/www/html/modules \
           drupal:8.2.1-apache

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

###### Tools used: [oh my zsh](http://ohmyz.sh/) / [reveal.js](https://github.com/hakimel/reveal.js) / [Simple Docker UI for Chrome](https://github.com/felixgborrego/docker-ui-chrome-app) / [docker compose 1.7.1](https://github.com/docker/compose/releases/tag/1.7.1) / [docker 1.11.1](https://github.com/docker/docker/releases/tag/v1.11.1)
