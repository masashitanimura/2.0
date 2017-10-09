---
title: Quick Start Guide on Windows
keywords: quick start guide
sidebar: home_sidebar
permalink: /home_quickstartguidewindows.html
folder: home
toc: true
---

## Purpose

This document provides instructions on how to install EvoStream Media Server (EMS) on Linux operating systems.
The document also provide instructions for some basic features of the EMS such as starting EMS, pulling, playing source streams and shutting down EMS.



## Getting EvoStream Media Server

1. Download the EMS package installer at <https://evostream.com/software-downloads>

2. Install EMS

   2.1. Extract the zip package

   2.2. Right-click on `setup.exe` then click **Run as administrator**

   ![](images/userguide/qsgfw1.jpg)

   ​

   2.3. Select the Setup Language, click **OK**

   ![](images/userguide/qsgfw2.jpg)

   ​

   2.4. Click **Next** to continue the installation

   ![](images/userguide/qsgfw3.jpg)

   ​

   2.5 Read the license agreement and select **I accept the agreement**, click **Next**

   ![](images/userguide/qsgfw4.jpg)

   ​

   2.6. Verify the installation path, click **Next**

   ![](images/userguide/qsgfw5.jpg)

   ​

   2.7. Tick **Create a desktop icon**, click **Next**

   ![](images/userguide/qsgfw6.jpg)

   ​

   2.8. Confirm installation, click **Install**

   ![](images/userguide/qsgfw7.jpg)

   ​

   2.9. Read the information, click **Next**

   ![](images/userguide/qsgfw8.jpg)

   ​

   2.10. Click **Finish** to finish the installation.

   ![](images/userguide/qsgfw9.jpg)

   ​

   **Note:** Uncheck **Launch EMS** if the license is not yet installed.



## License Installation

**Note:** You should already have your license file available. If none, EvoStream offers a **30-day free trial** license to those who want to explore the features of EMS. Click [here](https://evostream.com/free-trial/) to avail the free trial or contact [salesupport@evostream](mailto:salessupport@evostream.com) for other license type purchase.

To install the license, simply copy the `License.lic` file to `C:\EvoStream\config`.



## Starting EvoStream Media Server

To start EMS, simply **double click on the shortcut icon** of EMS or double click on `run_console_ems.bat` in the installed EMS folder.

![](images/home/startupicon.JPG)



The shortcut icon calls the `run_console_ems.bat`. You may also run this executable found in the installed EMS. Simply double-clicked to start the server. This script simply runs the Media Server through the command prompt, using `config/config.lua` as the main server configuration.

The EMS will open a console:

![](images/userguide/start1.png)



To check running applications, open the Task Manager and you should see:

```
evostreamms.exe
evo-node.exe    (for webserver)
evo-node.exe    (for webui)
evo-node.exe    (for webservices)
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



## Stream Playback Using UI

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



## Stopping the EMS server

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

