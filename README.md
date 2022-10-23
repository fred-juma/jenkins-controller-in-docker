# Installing Jenkins Controller in a docker image using docker compose 

#My Environment
* CentOS 8 Virtual machine
* Docker version 20.10.20 Installed
* Docker Compose version 1.25.0 installed 

## Project Structure

```bash
.
├── docker-compose.yml
└── README.md

0 directories, 2 files

```
## docker-compose.yml

```yaml
version: "3"
services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins-controller
    ports:
      - 8000:8080
      - 50001:50000
    volumes:
      - jenkins_home:/var/jenkins_home/
volumes:
  jenkins_home:
```

## Deploy the jenkins container with docker compose

Run the docker compose command to deploy the container in detatched mode

```bash
$ docker-compose up -d
Creating network "jenkins-controller-in-docker_default" with the default driver
Creating volume "jenkins-controller-in-docker_jenkins_home" with default driver
Creating jenkins-controller ... done
```

## Verify that the docker container is created and running
```bash
$ docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                                                                             NAMES
681fe8783532   jenkins/jenkins:lts   "/usr/bin/tini -- /u…"   36 minutes ago   Up 36 minutes   0.0.0.0:8000->8080/tcp, :::8000->8080/tcp, 0.0.0.0:50001->50000/tcp, :::50001->50000/tcp          jenkins-controller
```
## Launch browser to access the jenkins web interface.
0.0.0.0:8080

## Fetch the First time Administrator password available inside the container

```bash
$ docker exec jenkins-controller cat /var/jenkins_home/secrets/initialAdminPassword
a09578075c794b60a15b75dc6fb036f9
```

