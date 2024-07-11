# DevOps-Project-1-CICD

## Project Overview
Create a CICD Pipeline using Jenkins, Docker, Kubernetes

### Create Jenkins server
1. Setup an ec2 on AWS with custom security group of port 8080
2. ssh into the ec2 on a terminal (Gitbash)
3. install jenkins:
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
4. install java: 
```bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)
```
5. Start up jenkins:
```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```


### Dockerfile setup
1. Create a dockerfile in the app root directory. This will be used to create the docker image
```dockerfile
# syntax=docker/dockerfile:1

FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

COPY . .

RUN npm install

USER node

EXPOSE 3000

CMD node app.js
```

2. Test the dockerfile to see if it runs the app