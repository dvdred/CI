# CI
Continuos Integration


# Stack:
## - gitlab
## - jenkins
### (jenkins can be configured to connect to local docker daemon to spawn slaves)
## - tomcat (QA)
## - tomcat (PROD)
## - jenkins slave
### as a spawning contaienr, exiting 0 during compose up


# Persistent data:
## All the persistent data goes in i```./data``` folder, created during the firs build. For backup purpose just stop running composition and compress that folder.
### ./data is not tracked in git commits cause is present in .gitignore


# Default credntial:
## 1) Gitlab
### - None, ```admin``` is initialized on the first access
## 2) Jenkins: 
### - Default (read documentation)
## 3) Jenkins slave:
### - use jenkins master ssh key
## 4) Tomcat QA:
### - ```tsnapmanager:tsnappassword```
## 5) Tomcat PROD:
### - ```tmanager:tpassword```


# Tips
## - hosts file, add next lines in ```/etc/hosts``` to use names outside of the containers:
```
127.0.0.1       gitlab jenkins gitlab.local jenkins.local tomcat.dev tomcat.prod
```
## - ssh config: add next lines in ```~/.ssh/config``` to make easyer use gitlab:
```
Host gitlab.local
    Port 1122
```
