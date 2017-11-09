---
title: EMS Docker Image
keyword: liststreams
sidebar: userguide_sidebar
permalink: userguide_active.html
folder: userguide
toc: true
---

**Docker** is an open platform for developers and sysadmins to build, ship, and run distributed applications, whether on laptops, data center VMs, or the cloud. - Docker [website](https://www.docker.com/)

This is a simplified document on how to build and run Docker images for EMS 2.0.0 on Ubuntu 16.04. This document does not attempt to explain the concepts behind Docker. For a detailed explanation on Docker, please refer to the [official Docker documentation](https://docs.docker.com/).

**Pre-requisite:**

- Installed Docker

1. Run Docker

   ```
   $ sudo su
   # dockerd &
   # exit
   ```

   **Notes:** 

   - The Docker is run as daemon
   - The `#` prompt is shown while in privileged (or root) mode. The `$` prompt is shown while in non-privileged (or user) mode. In the commands below, `sudo` may be omitted if in privileged mode
   - Check docker if running by sending `ps -e|grep docker`

2. Run the pre-built Docker Image for 2.0

   ​