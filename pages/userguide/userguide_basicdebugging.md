---
title: Basic Debugging
keywords: debug
sidebar: userguide_sidebar
permalink: userguide_basicdebugging.html
folder: userguide
toc: true
---

## Unable to Run EMS

**Debug:**


1. **Check your License if already installed**. Maybe you forget to place your License file before running EMS. 
2. **Check your License if already expired**. You can no longer use EMS if your license is expired.
3. **Check if there are ports used by other applications**. There are many ports used by EMS, make sure that it is dedicated to EMS otherwise, there may be some errors with the connections.
4. **Check if you have a network connection**. If your license is an online type, EMS won't be able to connect to the License Manager who will verify your license.
5. **Check if you have a running instance of EMS.** You cannot run EMS simultaneously.
6. **Check if EMS is installed properly**. There may be some components that were not installed.
7. **Check Date and Time.** Date and Time should be the actual date and time. EMS will not run if it detects that date and time is adjusted.
8. **Check your Text Editor.** If you make changes in your config.lua file, make sure that you use a text editor that will not add additional characters on the file. This will corrupt the file and EMS will not run if the config.lua is corrupted.


------



## Pulled/Pushed Stream is not Streaming

**Debug:**

1. **Do preliminary checking**. Test you stream source by playing first on a player before pulling/pushing.

2. **Check if the stream is already pulled by sending `listConfig`**. The status should be **streaming** not connecting.

   ``` 
       pull:
         --
           configId: 1
           localStreamName: testpullStream
           status:
             current:
               description: Streaming
               uniqueStreamId: 1
           uri: rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4
   ```

3. **Check if the address of the server to push in is correct**. EMS will only look for the target address so make sure that the address in the API call is correct.

4. **Check if the localStreamName is correct.** EMS will search for the localStreamName in the API call, the stream will not be pushed if localStreamName is not found.


------




## Stream is Not Recording

**Debug:**

1. **Do preliminary checking**. Test you stream source by playing first on a player before recording.
2. **Make sure your pathToFile value is writable**. EMS will not able to record if the path given is read-only.
3. **Check if your network connection is stable**. There might be a problem occur when the network connection is not stable.


------



## Unable to Run Web UI

**Debug:**

1. **Check config.lua.** Check if `runWebUI` is set to `false`. It should be set to `true`.
2. **Check port availability**. Make sure that the port that UI listens to is available.


------




## Unable to Stream VOD from Web UI

**Debug:**

1. **Check Flash.** Make sure that Flash is set to Allow in the browser.

   ![](images/userguide/debug_flash.jpg)

   ​

2. **Please Use Google Chrome.**  The Video. Js player is not supported in Firefox, therefore, the stream will not be played. 


------




## Unable to Stream HLS from WebUI

**Debug:**

1. **Please Use Google Chrome.**  The Video. Js HLS build player is not supported in Firefox, therefore, the stream will not be played. 

------

