---
title: Using EMS on Docker
keyword: docker
sidebar: userguide_sidebar
permalink: userguide_docker.html
folder: userguide
toc: false
---

**Docker** is an open platform for developers and sysadmins to build, ship, and run distributed applications, whether on laptops, data center VMs, or the cloud. - Docker [website](https://www.docker.com/)

This is a simplified document on how to build and run Docker images for EMS 2.0.0 on Ubuntu 16.04. This document does not attempt to explain the concepts behind Docker. For a detailed explanation on Docker, please refer to the [official Docker documentation](https://docs.docker.com/).



## Running EMS on Docker

**Pre-requisite:**

- Installed Docker

**Steps:**

1. **Pull** the EMS docker image:

   ```
   sudo docker pull evostream/<EMS version>-<OS>:<build number>

   sample:
   sudo docker pull evostream/ems201-ubuntu1604:5649
   ```

   **Available images:**

   - evostream/ems200-ubuntu1604:5550


   - evostream/ems201-ubuntu1604:5649

   **Note:** You can check the available images in the [Docker store](https://store.docker.com)

   ​

2. **Run** Docker from the console in privileged mode.

   ```
   $ sudo su
   # dockerd &
   # exit
   ```

   **Notes:** 

   - The Docker is run as daemon
   - The `#` prompt is shown while in privileged (or root) mode. The `$` prompt is shown while in non-privileged (or user) mode. In the commands below, `sudo` may be omitted if in privileged mode
   - Check docker if running by sending `ps -e|grep docker`

   ​

3. **Test** Docker

   Run the "hello world" demo to test your Docker installation. You may remove the "hello world" image afterwards.

   ```
   $ sudo docker run --name hello hello-world
   $ sudo docker ps -a
   $ sudo docker images
   $ sudo docker rmi hello-world
   ```

4. **Run** the EMS Docker Image

   Run the script below to use the pre-built Docker image for EMS on the EvoStream public repository on Docker Hub.

   ```
   sudo docker run --name <container_name> -i -t -p \
     -p 1112:1112/tcp \
     -p 1222:1222/tcp \
     -p 1935:1935/tcp \
     -p 4000:4000/tcp \
     -p 4100:4100/tcp \
     -p 5544:5544/tcp \
     -p 6666:6666/tcp \
     -p 7777:7777/tcp \
     -p 8080:8080/tcp \
     -p 8100:8100/tcp \
     -p 8210:8210/tcp \
     -p 8410:8410/tcp \
     -p 8433:8433/tcp \
     -p 8888:8888/tcp \
     -p 9898:9898/UDP \
     -p 9998:9998/tcp \
     -p 9999:9999/tcp \
     <image_name> bash
   ```

5. **Login** to container

   If you are not automatically logged in to the container, send the command below:

   ```
   sudo docker exec -i -t <container_id> /bin/bash

   sample:
   sudo docker exec -i -t 3cb068bca5b6 /bin/bash
   ```

   **Note:**  The prompt changes to `root@<instance_id>`  successful login.

   ​

6. **Start** EMS

   The Docker image doesn't include an EMS license. You may obtain a trial license from the [EvoStream website](http://evostream.com/). From your host machine, copy the license file `License.lic` to `/etc/evostreamms` or `/config` folder in the container.

   ```
   $ sudo docker cp /path/to/License.lic <container_name>:/etc/evostreamms

   sample:
   $ sudo docker cp /path/to/License.lic evostream/ems201-ubuntu1604:5649:/etc/evostreamms
   ```

   Use the `sudo docker ps -a` command to check the container names of running instances.

   Inside the Docker container, start the EMS (in privileged mode):

   ```
   # service evostreamms start
   ```
