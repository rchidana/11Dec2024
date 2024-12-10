# First create a Docker managed volume

```
docker volume create jenkins-config
docker volume ls
docker inspect jenkins-config

docker run -p 8080:8080 -v jenkins-config:/var/jenkins_home -d jenkins/jenkins:lts-jdk17
docker logs <container-name>

```
Check the IP address of your machine + open a browser --> http://IP-OF-YOUR-MACHINE:8080

YouTube Link : --> https://youtu.be/isLjgFio5a8?si=Bl3SR1q31GnqTmNp
