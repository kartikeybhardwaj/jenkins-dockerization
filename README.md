# Jenkins Dockerization

#### Plan of action

1. Pull Jenkins image
2. Write docker-compose file
3. Execute Jenkins container

#### Pull Jenkins image

    docker pull jenkins/jenkins:lts

Show pulled image by executing

    docker images

#### Write docker-compose file

    version: "3.7"

    services:

    jenkins:
        image: jenkins/jenkins:lts
        container_name: jenkins
        restart: unless-stopped
        ports:
        - 8080:8080
        - 50000:50000
        volumes:
        - ./jenkins_home:/var/jenkins_home

##### Explanation of docker-compose file
- `version` is a version of docker-compose file format, you can change to the latest version.
- `jenkins` on line 5 is just a service name, you can change the name whatever you want.
- image must be **jenkins/jenkins:lts**, because you want to create a container from its image.
- `container_name` is a name for your container, it’s optional.
- `volumes` to define a file/folder that you want to use for the container.
- `./jenkins_home:/var/jenkins_home` means you want to set data on container persist on your local folder named **jenkins_home**. **/var/jenkins_home/** is a folder that already created inside the Jenkins container.
- `ports` is to define which ports you want to expose and define, in this case we're using default Jenkins port **8080**.

#### Execution

Now run the docker-compose file with `docker-compose up` or `docker-compose up -d` to run containers in the background.

Open another terminal to login to the container. Type `docker ps` to see our running container.

#### References
- [Jenkins](https://jenkins.io/)
- [Compose file version 3 reference | Docker Documentation](https://docs.docker.com/compose/compose-file/)