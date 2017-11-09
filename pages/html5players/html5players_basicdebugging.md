---
title: Basic Debugging
keywords: html5
sidebar: html5players_sidebar
permalink: html5players_basicdebugging.html
folder: html5players
toc: true
---

## Unable to Play using WebSockets/WebRTC

**Debug:**

1. **Do preliminary checking.** Test you stream source by playing first on a different player.

2. **Check HTML 5 browser support.** You may check the support by clicking on this [link](https://www.youtube.com/html5?gl=PH). H.264 and MSE & H.264 should be checked.

   If using Firefox, please change the following configurations:

   ```
   1. In the Firefox address field enter: about:config
   Click “I’ll be careful I promise!”

   2. Locate the following variables and set them (double-click) as necessary to match:
   media.mediasource.enabled = true
   media.mediasource.whitelist = false
   media.mediasource.mp4.enabled = true
   media.fragmented-mp4.exposed = true
   media.fragmented-mp4.ffmpeg.enabled = true
   media.fragmented-mp4.gmp.enabled = true
   media.fragmented-mp4.use-blank-decoder = false

   3. Restart Firefox to activate the changes
   ```

3. Check if the connection has been established.** Normally, when a browser was able to establish connection with EMS, the EMS logo would appear on the HTML5 player. If no logo appeared, then that means it wasn’t able to connect with EMS because the connection was not established or EMS was not able to successfully establish a data channel. For this scenario, For WebRTC, check that EMS has started webRTC and that you are using the correct room or send the EMS logs to EvoStream support team.

4. **Check if stream is available.** In this case, the logo of EvoStream would appear and would just be stuck there. If you ticked on the “Show debug messages” **IMMEDIATELY RIGHT AFTER** loading the webRTC page, a couple of logs such as these can be seen:

   ```
   1453259850224: Media source is now ready.
   1453259850224: Command: {"payload":{"description":"Requested stream could not be sent!","name":"myStream", "status":"FAIL"},"type":"fmp4Response"}
   1453259850222: channelOpen emsStreamChannel
   1453259850221: Sending request for fmp4...
   1453259850221: channelOpen emsCommandChannel
   1453259850219: Connection established with qKbPr2FJHicfvNx6xRP0

   ```

   The log means, although connection was indeed established, the stream that is being requested is not available.

------



## Flickering and/or Freezing of the Video Using HTML5 player

**Debug:**

1. **Adjust GOP size.** This is likely caused by a too-small video buffer. In the page JS you can modify the queueSize variable to control the size of that buffer. It is a variable in the option parameter you send to the EvoWsPlayer function/constructor. In the source code from this example [page](http://ers.evostream.com:5050/demov2/evoplayers.html):

   The options variable should look like this:

   ```
   var opts = {
   		emsIp: emsIp,
   		streamName: streamName,
   		videoTagId: 'video' + number,
   		debugDivId: 'debug' + number,
   		queueSize: 5
   		};

   ```

   queueSize is measured in GOP’s. The higher the GOP size, the less buffer it has but take note that it will also increase the size of footprint in your computer. The important thing to note is that this will increase playback latency!