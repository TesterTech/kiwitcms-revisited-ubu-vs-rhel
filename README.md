# kiwitcms-revisited-ubu-vs-rhel
Code for the YouTube video: https://youtu.be/S7h4OG7aeFA

## Command executed in the terminal

Note: 
- all commands are executed as root 
- to go into root type: ```sudo -s``` or ```sudo su -```

Ubuntu 18.04
- Optional if you want to connect to this VM using sshclient:
```
 sudo apt install openssh-server
```
```
snap install docker
git clone --depth 1 https://github.com/kiwitcms/Kiwi.git kiwi-tcms/
cd kiwi-tcms
docker pull kiwitcms/kiwi
docker-compose up -d
docker exec -it kiwi_web /Kiwi/manage.py initial_setup

```
RHEL 8.3
```
sudo dnf install -y git vim-enhanced wget 
sudo dnf install -y podman-docker
git clone --depth 1 https://github.com/kiwitcms/Kiwi.git Kiwi
cd Kiwi
docker pull kiwitcms/kiwi
wget https://raw.githubusercontent.com/kiwitcms/Kiwi/master/docker-compose.yml
pip3 install docker-compose
pip3 install --upgrade pip
pip3 install setuptools --upgrade
pip3 install wheel
sudo /usr/local/bin/docker-compose up -d
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


