# Jenkins-Ansible

<sub/> 

Installing Ansible. We are gonna work in our Jenkins container. 

```
mkdir jenkins-ansible
cd jenkins-ansible
nano Dockerfile
```

<img width="650" alt="Zrzut ekranu 2023-07-23 o 11 33 22" src="https://github.com/eda6767/Jenkins-Ansible/assets/102791467/b53db909-6b35-4b11-9500-aa558c97ccff">

Also we need to update the docker-compose.yml file for jenkins container.

<img width="650" alt="Zrzut ekranu 2023-07-23 o 11 14 44" src="https://github.com/eda6767/Jenkins-Ansible/assets/102791467/e457adb4-7ce6-4bed-b019-d3edc4ea624a">

```
docker-compose up -d
docker ps
```
To verify the installation on Ansible, let's logg into jenkins container:


```
docker exec -ti jenkins bash
ansible
```

