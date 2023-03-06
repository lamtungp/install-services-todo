<h2><bold>MongoDB</bold></h2>

**1. Create an User**

```
db.createUser( { user: "admin", pwd: "tracking", roles: [ { role: "readWrite", db: "tracking" } ] }, { w: "majority" , wtimeout: 5000 } )
```
**2. Restore**
```
mongorestore --host=${dbHost} --port=${dbPort} --username=${dbUser} --authenticationDatabase={dbAuthSource} ${folderRestore}
```

<h2><bold>Docker</bold></h2>

**1. Create PhpMyAdmin container**

```
docker run --name myadmin -d -e PMA*HOST=dbhost -e PMA* USER=dbuser -e PMA_PASSWORD=dbpassword -p 8080:80 phpmyadmin
```

<h2><bold>Kubectl</bold></h2>

**1. Port-forward**
```
Step 1: Prepare
- Be sure that computer installed docker and kubectl. If dont have kubectl, install it by: https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/
- Be sure have kube config cluster in ~/.kube, ex: ~/.kube/staging-config

Step 2: Use Command:
sudo nano /etc/hosts
Paste this line into file above:
10.0.0.218 kubernetes.default.svc.zinza.tracking

Step 3: Use kubectl to port forward:
export KUBECONFIG=~/.kube/<config_file_name>
kubectl port-forward svc/mongodb 27020:27017 -n tracking

Step 4: Now, you can connect to db with info:
Host: localhost
Port: 27020
Database: tracking
Ex: mongodb://username:password@localhost:27020
```

- Fix: Bash script and /bin/bash^M: bad interpreter: No such file or directory
  sed -i -e 's/\r$//' scriptname.sh
