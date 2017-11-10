---
title: Connecting to EMS
keywords: azure
sidebar: emscloud_sidebar
permalink: emscloud_azure_connectEMS.html
folder: emscloud
toc: true
---



## Starting the EMS Machine

All the virtual machines in your account is seen under the Virtual machines in the left-side menu bar. 

Click on the Virtual Machine name. Click on **Start**.

![](images/emscloud/startVM.JPG)



## Connecting To EMS

After starting the EMS instance, you will need to connect to your EMS to use it. Here are the steps on how you can connect to EMS using **SSH Terminal**, **Windows PuTTy**, **Remote Desktop**, **EMS Web UI** and **EMS HTTP Based API**.



### SSH via Terminal

1. Send command: `ssh <username>@<IP_address>`

   ```
   user@ubuntu:~/Desktop$ ssh user@11.221.105.202

   The authenticity of host '111.221.105.202 (111.221.105.202)' can't be established.
   RSA key fingerprint is ae:02:ee:41:ff:38:96:ab:78:7b:3a:e6:09:ed:1f:4c.
   Are you sure you want to continue connecting (yes/no)? 
   ```

2. Input "**yes**", press **Enter**

   ```
   Warning: Permanently added '111.221.105.202' (RSA) to the list of known hosts.
   user@111.221.105.202's password:
   ```

3. Enter password, press **Enter**. You can now use EMS capabilities!


**Note:** EMS is already running. You can check it by sending ps -e|grep evo

```
$ ps -e|grep evo
  4627 pts/0    00:00:01 evostreamms
  4628 pts/0    00:00:00 evo-node
  4629 pts/0    00:00:00 evo-node
  4635 pts/0    00:00:01 evo-node
```



### Connecting  via SSH from Windows (PuTTy)

**Pre-requisites:**

- PuTTY Secure Shell Client

  ​


1. Run **PuTTY**

2. Select **Session** under the category tree

   ![](images/emscloud/image16.png)

   ​

3. Specify the destination you want to connect to:

   ![](images/emscloud/putty.JPG)

   **Host Name** – the public IP address in Amazon EC2 instance running EvoStream Media Server

   **Port** – 22 (default)

   **Connection type** – SSH

   ​

4. Click **Open**

5. Click  **Yes** to accept the security key on the PuTTy Security Alert Window

6. Enter the username's password, hit **Enter**

   ```
   Using username "EvoStream".
   EvoStream@111.221.105.202's password: 
   ```

7. You are now connected to the machine! 




### HTTP Based API

For the EMS on Azure, the HTTP based API is exposed, but it requires authentication to be used.  We call this **Proxy Authentication**. Basic Authentication is used and so just a username and password are required:

- Username: evostream
- Password: "UID" - the unique identifier of the virtual machine, this will be seen in webconfig.lua

**Command will take this general format:**

```
http://Username:Password@IPAddress:Port/apiproxy/CommandName?params=<base64EncodedString>
```

Run the command in a browser. 

**Sample Command:** 

```
http://evostream:i-D817E76F-B6F2-CC4F-ACAC-EAE9D84CEE3F@52.91.237.115:8888/apiproxy/version
```

**Note:** username is “**evostream**” and password is the “**instance ID**”

See EMS [HTTP JSON CLI](userguide_telnet.html#http-json-cli) for more details.



#### Getting the Unique ID

The UID will serves as the password for the Proxy and Web UI authentication. The UID is obtained once a virtual machine is made. It can only be checked in the EMS webconfig.lua.

**in webconfig.lua:**

```
apiProxy=
{
   authentication="basic",
   pseudoDomain="apiproxy",
   address="127.0.0.1",
   port=7777,
   userName="evostream",
   password="D817E76F-B6F2-CC4F-ACAC-EAE9D84CEE3F",   --> sample UID
}
```