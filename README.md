# Learn docker


# Docker lecture 1 - Manual process to create container and Dockerfile
- 29
    ```
        systemctl start docker
        systemctl enable docker
        systemctl status docker

        docker pull ubuntu
        docker run -it --name cont1 ubuntu

        apt update
        apt install apache2 mysql-server python3 -y

        docker info 
        CTRL + D => stop cont1

        docker ps -a 
        docker start cont1
        docker exec -it cont1 /bin/bash
            - i interactive
            - t - allocates a pseudo TTY
            - /bin/bash - specifies the command to run inside the container 

        CTRL + p+ q 
    ```
- OS level virtualisation - take the complete backup of OS and install the same stack on another OS
    - Install the same stack from cont1 (custom image) to another container, cont2
    - Instead of pulling the images and installing everything again, use backup of the container
    - docker commit - create a new image from a container

    ```
        docker images
        docker rmi -f: This command forcefully removes the images with the specified IDs.
        docker commit containerBaseImageName newImageName
        e.g. docker commit cont1 custom_image:v1
    ```
- Create a new image from custom_image:v1 : `docker run -it --name cont2 custom_image:v1`
    - `apache2 -v`
    - `mysql --version`
    - `python3 --version`

- Dockerfile 
    - Instead of manually creating the image, we can create the image using Dockerfile
    - Automate the process 
    - Dockerfile is a text file that contains a set of instructions for building a Docker image.
    - D - must be capital
    - Components must also be Capital.

    ```
        docker kill $(docker ps -qa)
        docker rm $(docker ps -qa)              ==> Remove all containers
        docker rmi -f $(docker images -qa)      ==> rmi is for removing images and -f (force): Force the removal of the image even if it is being used by a container.
        docker stop $(docker ps -aq)             ==> Stop all containers
        docker stop $(docker ps -q)
        docker ps -q  ==>q (quiet): Only display the numeric IDs of the containers.
    ```
- Components
