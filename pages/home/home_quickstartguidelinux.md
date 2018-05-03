---
title: Quick Start Guide on Linux
keywords: quick start guide
sidebar: home_sidebar
permalink: /home_quickstartguidelinux.html
folder: home
toc: true
---

## Purpose

This document provides instructions on how to install EvoStream Media Server (EMS) on Linux operating systems.
The document also provide instructions for some basic features of the EMS such as starting EMS, pulling, playing source streams and shutting down EMS.



## Getting EvoStream Media Server

### Linux Archive

1. Download the EMS tarball at https://evostream.com/software-downloads

2. Extract the .tar.gz file to install the EMS at a directory of your choice.

  ​

### APT/YUM

**Pre-requisite:**
Administrative privileges are required. This can be accomplished in many ways.
If the sudo utility is available:

```
$ sudo su –
```

If the sudo utility is not available:

```
$ su –
```

**Note:**

The prompt changes from ‘$’ to ‘#’ when administrative privileges are enabled.



**Installation:**

1. Retrieve the script used to install the EvoStream software repository and store it

   - Debian based Linux distributions (Ubuntu or Debian)

     ```
     # wget http://apt.evostream.com/installkeys.sh -O /tmp/installkeys.sh
     ```

   - RedHat based Linux distributions (CentOS, Fedora, RHEL)

     ```
     # curl http://yum.evostream.com/installkeys.sh -o /tmp/installkeys.sh
     ```

     ​


2. Execute the script to install the EvoStream software repository and keys

   ```
   # sh /tmp/installkeys.sh
   ```

   If successful, the following message should be printed on the console:

   ```
   "EvoStream keys installed successfully"
   ```

   ​

At this stage, the EvoStream software repository and keys are successfully installed and you can install packages from it.

**Note:** Steps 1 and 2 above must be executed only once.

The following steps are used to install the EvoStream Media Server, and can be repeated to update the EMS to the most recent release.



3. Install EvoStream Media Server.

   - Debian based Linux distributions (Ubuntu or Debian)

     ```
     # apt-get install evostream-mediaserver
     ```

   - RedHat based Linux distributions (CentOS, Fedora, RHEL)

     ```
     # yum install evostream-mediaserver
     ```

     ​




## License Installation

**Note:** You should already have your license file available. If none, EvoStream offers a **30-day free trial** license to those who want to explore the features of EMS. Click [here](https://evostream.com/free-trial/) to avail the free trial or contact [salesupport@evostream](mailto:salessupport@evostream.com) for other license type purchase.

Simply place the License.lic file in the following location:

### Linux Archive

```
../config
```



### APT/YUM

```
/etc/evostreamms/
```

**Note:**
EMS will read first the /etc/evostreamms path for the License upon start-up. Make sure to check your License if you have an apt/yum installed and you run an archive.



## Starting EvoStream Media Server

### Linux Archive

You may run EMS via following:

1. Open a terminal

2. Locate the **EvoStream/bin folder**

3. Send **./run_console_ems.sh**

   ![](images/userguide/start1.png)

   ​

4. Check in terminal if EvoStream is running by sending **`ps –e|grep evo`** command. You should see

  ```
  user@ubuntu:~$ ps –e|grep evo
  10727 pts/4 00:00:22 evostreamms
  10728 pts/4 00:00:05 evo-node (for webserver)
  10729 pts/4 00:00:00 evo-node (for webui)
  10730 pts/4 00:00:00 evo-node (for webservices)
  ```

  ​

### APT/YUM

You may run EMS via following:

1. Open a terminal

2. Send **`service evostreamms start_console`**

   ![](images/userguide/start1.png)

   ​

3. Check in terminal if EvoStream is running by sending **`ps –e|grep evo`** command. You should see:

  ```
  user@ubuntu:~$ ps –e|grep evo
  10727 pts/4 00:00:22 evostreamms
  10728 pts/4 00:00:05 evo-node (for webserver)
  10729 pts/4 00:00:00 evo-node (for webui)
  10730 pts/4 00:00:00 evo-node (for webservices)
  ```






## Connecting to Web UI

After successful start-up, you can now open the EMS Web UI.

1. Simply open **`<EMS_IP>:4100`** in browser

2. Create and/or login a user

   ![](images/home/UI_home.png)

3. You can now check the EMS functionalities!
  Click on this [link](http://docs.evostream.com/2.0/userguide_webuioverview.html) to know more on how to use the EMS Web UI.




## Basic EMS API

### pullStream using UI

1. Go to **Add** page in UI

2. Select pull command

3. Enter `rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4` in URI Stream Source

4. Enter `test` as a Local Stream Name

   ![](images/home/addstream.JPG)

   ​

5. Click **Add Stream**






### Stream Playback Using UI

Pulled streams are automatically saved in EMS. To play the pulled stream, use a media player that supports the media format that was pulled or simply use the UI to stream the pulled video source.

1. Go to **Active** Page in UI

2. Click on the **Play** button of the stream you want to play

   ![](images/home/playback.JPG)

   ​

EMS automatically converts the stream pulled in different protocols so no worries if you want to play the stream using an RTMP or RTSP protocol for example.
To play in media player:

1. Go to Open Network Stream

2. Enter the URL of the pulled stream

   - For RTSP: `rtsp://127.0.0.1:5544/test`

   - For RTMP: `rtmp://127.0.0.1/live/test`

     ![](images/home/rtspplayback.jpg)

     ​

The EMS will fetch the pulled stream via `localStreamName` and playback will start once the file is found.



### Stopping the EMS server

If the user wants to shut down the EMS, just send the command:

```
shutdownServer
```

The EMS will respond to a key:

```
shutdownServer
Command entered successfully!
Call shutdownserver again with the provided key
key: bvjvUo8HQ6VzDFJv
```

Then send the `shutdownserver` command with the key:

```
shutdownServer key=bvjvUo8HQ6VzDFJv
```

The EMS will shut down after sending the command.



Please refer to [EMS User Guide](http://docs.evostream.com/2.0/userguide_overview.html) and [EMS API Guide](http://docs.evostream.com/2.0/api_overview.html) for more information.

