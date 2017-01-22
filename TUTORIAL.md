# Rapid tutorial on jenkis-docker integration

## 1): Install plugins and connect to docker daemon:
### After inserting the auto generated password you will be asked to install the main plugins (choose them!) and to setup the administrator user.
### Generate a jenkins credential for the slaves: ```Credentials```. (username and password must be *"jenkins"*, leave at default other options)
### Go to the ```Manage Jenkins``` section, and go in the ```Plugin Manager```. Install the ```Docker Plugin``` (without restart). Then point back to the previous menu and you will see a new ```Docker``` section. Point instead to the firt section ```Configure Jenkins```. A the end of the page there is an option ```Add a new cluoud```. Press it.
### NOT WORKING: Put a name and the unix socket docker URL: ```unix:///var/run/docker.sock```, then press ```Test Connection```. (https://github.com/jenkinsci/docker-plugin/issues/439 and https://github.com/jenkinsci/docker-plugin/issues/471 )
### WORKING: Put a name and the tcp socket docker URL (for example, lets docker daemon listen on tcp://0.0.0.0:4243): ```tcp://127.0.0.1:4243``` then press ```Test Connection```. (*WARNING*: unsafe on untrusted lan, protect with tls isn't covered in this tutorial)
### Configure a docker image to spawn; ```ci_jslave``` (built after the first compose up)
### Configure labels: ```docker-slave```
### Configure usage: ```Only build jobs with label...```
### Configure Launch method: ```Docker SSH...```
### Add Credential: ```jenkins/****```
### Configure Remote FS Root Mapping: leave empty
### Apply and Save
### If previous steps are all good you will see container of the composition in ```http://jenkins.local:8080/docker-plugin/```

## 2): Build a docker image with jenkins and push to a registry
### TODO
