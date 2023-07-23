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

Now to make the SSH key pernament on the Jenkins container let's make subdirectory in $HOME directory and copy the remote-key file into this new subdirectory.

```
mkdir jenkins_home/ansible
cp centos/remote-key jenkins_home/ansible/
ls jenkins_home/ansible
```

### Create Inverntory for Ansible

```
cd jenkins-ansible
cp ../centos/remote-key .
nano hosts
```
<img width="994" alt="Zrzut ekranu 2023-07-23 o 11 52 29" src="https://github.com/eda6767/Jenkins-Ansible/assets/102791467/322874ac-ebf3-4550-8ea3-e099df2a58bf">


```
cp hosts ../jenkins_home/ansible/
```


Test connection:

```
docker exec -ti jenkins bash
ping remote_host
```

Unfortunatelly I have received an ERROR: ping: command not found, so I logged with root user into Jenkins container and install following package:

```
docker exec -u 0 -ti jenkins bash
apt-get update
apt-get install -y iputils-ping
exit
```

And logged again:

```
docker exec -ti jenkins bash
ping remote_host
```


```
ansible all --list-hosts
ansible -i hosts -m ping test1
```

### Ansible Playbook

```
cd jenkins-ansible
nano play.yml
```

<img width="929" alt="Zrzut ekranu 2023-07-23 o 13 28 38" src="https://github.com/eda6767/Jenkins-Ansible/assets/102791467/c791ccbf-870c-4087-8181-6de5b63ef815">



```
cp play.yml ../jenkins_home/ansible/
docker exec -ti jenkins bash
cd /var/jenkins_home/ansible
ansible-playbook -i hosts play.yml
```


<img width="993" alt="Zrzut ekranu 2023-07-23 o 13 29 24" src="https://github.com/eda6767/Jenkins-Ansible/assets/102791467/3cf9dbfd-9bff-4c7a-a52c-5af85cd4d761">


