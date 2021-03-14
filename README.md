# kiwitcms-revisited-ubu-vs-rhel
Code for the YouTube video: https://youtu.be/S7h4OG7aeFA

## Command executed in the terminal

Ubuntu 18.04
```
Optional if you want to connect to this VM using sshclient: sudo apt install openssh-server
```
Note: 
- all commands are executed as root 
- to go into root type: ```sudo -s``` or ```sudo su -```

```
docker pull kiwitcms/kiwi
snap install docker
mkdir kiwi && cd kiwi
wget https://raw.githubusercontent.com/kiwitcms/Kiwi/master/docker-compose.yml
docker-compose up -d
docker exec -it kiwi_web /Kiwi/manage.py initial_setup
```
RHEL 8.3
```
dnf install -y git vim-enhanced wget 
dnf install -y podman-docker
mkdir kiwi && cd kiwi
docker pull kiwitcms/kiwi
wget https://raw.githubusercontent.com/kiwitcms/Kiwi/master/docker-compose.yml
pip3 install docker-compose
pip3 install --upgrade pip
pip3 install setuptools --upgrade
pip3 install wheel
pip3 install docker-compose
/usr/local/bin/docker-compose up -d
 sudo systemctl start podman.socket
 sudo curl -H "Content-Type: application/json" --unix-socket /var/run/docker.sock http://localhost/_ping
```

References:
- https://kiwitcms.readthedocs.io/en/latest/
- https://kiwitcms.readthedocs.io/en/latest/installing_docker.html
- https://github.com/ChameleonCloud/CC-Ubuntu/commit/b42d364a15c41c2f73515539bde31f6e9b723611 (if you have the issue with cryptography when installing docker-compose in pip3)
- https://www.redhat.com/sysadmin/podman-docker-compose (podman / docker / etc)
- https://www.youtube.com/watch?v=cGPqOafMFkE (previous video on ootb experience in OSS projects)
- https://youtu.be/QTkkcDrDk6Q?t=91 (an old testertech video about cgroups v2 and fedora and playing around with some workarounds, etc)


