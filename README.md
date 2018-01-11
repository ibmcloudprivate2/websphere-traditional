# Local Machine Docker

## Image location
[ibmcom/websphere-traditional](https://hub.docker.com/r/ibmcom/websphere-traditional/)

# Pull the Image
```
docker pull ibmcom/websphere-traditional
```

## Run it
```
docker run --name test -h test -p 9043:9043 -p 9443:9443 -d ibmcom/websphere-traditional
```

## Access it
Console (https://localhost:9043/ibm/console)
```
id: wsadmin
```
to obtain the password for the login, run the following command
```
docker exec test cat /tmp/PASSWORD
```

## List the Docker container
```
docker ps
```

# Deploy websphere-traditional on IBM Cloud Private

## Push image to ICP
```
docker login mycluster.icp:8500
```

## tag the Image
```
docker tag ibmcom/websphere-traditional mycluster.icp:8500/jaricdev/ibmcom/websphere-traditional:9.0.0.6
```

## Push the Image
```
docker push mycluster.icp:8500/jaricdev/ibmcom/websphere-traditional:9.0.0.6
```

## Deploy the Image

General Tab

name | value
-----| -----
Name | js-websphere-traditional

Container settings Tab

name | value
-----| -----
Name | js-websphere-traditional
Image | mycluster.icp:8500/jaricdev/ibmcom/websphere-traditional:9.0.0.6
Container port | 9043, 9443


# Expose the deployment with Service

General Tab

name | value
-----| -----
Name | js-websphere-traditional
Type | NodePort

Ports Tab

name | value
-----| -----
TCP | http, 9043, 9043
TCP | https, 9443, 9443

Selectors Tab

name | value
-----| -----
app | js-websphere-traditional

# Access the console

From the service link, append '**ibm/console**'
Example
```
https://192.168.64.220:30412/ibm/console/logon.jsp
```

192.168.64.220 is the url of ICP.

# Obtaining the password
Find out the pod name and run the, you will need to configure the kubectl using ICP context info.

```
kubectl exec <podname> -it cat /tmp/PASSWORD
```

e.g. replace <podname> with **js-websphere-traditional-2986188259-15lxd**

# References
WebSphere traditional application server for developer
- https://hub.docker.com/r/ibmcom/websphere-traditional/
