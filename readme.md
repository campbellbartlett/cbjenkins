# cbjenkins
## Project I've been working on to containerise a jenkins set up for my own personal use.

It creates 3 containers and combines everything into a docker-compose.

The container are:
- jenkins-master
- jenkins-data
- jenkins-nginx

###### jenkins-master
The container that runs jenkins. Almost all settings are left to default, with the
exception of --logfile which stores the log at /var/log/jenkins/jenkins.log and
the webroot which is moved to /var/cache/jenkins/war.
The webroot is moved so that the other settings can be kept between docker builds
without the unecessary war file.

###### jenkins-data
A data only container. Runs debian:jessie, sets up two folders and mounts them 
for use by other containers and stops.
The folders are:
- /var/log/jenkins/ so that the jenkins log is persisted across multiple builds and
- /var/jenkins_home to persist the jenkins settings and jobs across builds

###### jenkins-nginx 
A simple nginx set up that makes jenkins available at port 80

###### How to build:
```
docker-compose build
```

###### How to start:
```
docker-compose up -d
```

###### How to stop:
```
docker-compose stop
```

###### How to stop and remove everything stored in jenkins-data:
```
docker-compose stop
docker-compose rm
```

###### How to stop and remove everything except jenkins-data:
```
docker-compose stop jenkinsdocker_jenkinsnginx_1
docker-compose stop jenkinsdocker_jenkinsmaster_1
docker rm jenkinsmaster jenkinsnginx
```