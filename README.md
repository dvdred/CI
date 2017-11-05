# CI
### Continuos Integration

# Stack:
## - gitlab
## - jenkins master
### (jenkins can be configured to be connected to the local docker daemon)
## - tomcat (QA)
## - tomcat (PROD)
## - jenkins slave
### (as a spawning contaienr, exit 0 after  docker-compose up)


# Persistent data:
## All the persistent data goes in the ```./data``` folder. For backup purpose just stop running composition and save that folder.
### ./data is not tracked in git commits cause is present in .gitignore


# Default credential:
## 1) Gitlab
### - None, the password for the user ```admin``` is initialized on the first access
## 2) Jenkins: 
### - Auto generated during the firs start. (it will be printed in the jenkis master container logs)
## 3) Jenkins slave:
### - use jenkins master ssh key
## 4) Tomcat QA:
### - ```tsnapmanager:tsnappassword```
## 5) Tomcat PROD:
### - ```tmanager:tpassword```


# Tips
## - hosts file, add the next lines in ```/etc/hosts``` to use names outside of the containers:
```
127.0.0.1       gitlab jenkins gitlab.local jenkins.local tomcat.dev tomcat.prod
```
## - ssh config: add the next lines in ```~/.ssh/config``` to make easier use of gitlab:
```
Host gitlab.local
    Port 1122
```

# EXTRA
## - to configure jenkins master to connect to docker daemon with network socket, docker daemon must be configured to listen to the network.
### This is a sample with systemd dropin unit file. As root, copy and paste the next commands:
```
systemctl stop docker
mkdir /etc/systemd/system/docker.service.d/
```
```
# cat >"/etc/systemd/system/docker.service.d/daemon.conf"<<'EOF'
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H tcp://127.0.0.1:4243 -H unix:///var/run/docker.sock
EOF
```
```
systemctl daemon-reload
systemctl start docker
```
