## How to get Jenkins up and running inside Docker

These instructions will install and run a Jenkins container which will allow you to run Jenkins on your computer

Since we will be using "Docker agents" in the Jenkins pipeline, the Jenkins container will need to be able to access your local Docker server.  

Do do this we will open up permissions on the docker socket. 

**Warning: This is not a good thing to do in a production environment as it is not secure**

    sudo chmod 777 /var/run/docker.sock

Now we need to pull and run the Jenkins docker image:

```bash 
docker run -p 8080:8080 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --name jenkins \
  jenkins/jenkins
```

We now need to connect to the Jenkins container and install the docker CLI inside the container.  

Open a **new terminal** and type: 

    docker exec -it -u root jenkins bash

You are now connected to the Jenkins container and can issue bash commands inside the container.

This next step installs the Docker CLI in the Jenkins container.

Copy and paste the following:


    apt-get update && \
    apt-get -y install apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
        software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
    add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) \
    stable" && \
    apt-get update && \
    apt-get -y install docker-ce && \
    usermod -a -G docker jenkins



