---
title: Streaming Using WebRTC
keywords: webrtc
sidebar: html5players_sidebar
permalink: html5players_wrtcdemo.html
folder: html5players
toc: true
---

**Peer to Peer streaming uses the EvoStream HTML5 Streaming capabilities. It is recommended you also review the HTML5 Streaming section.**



## Using Demo Player

Starting release 2.0, the HTML5 web player of EMS or what we've called the evoplayers, can now play different streams such as: 

- Pulled RTMP/RTSP streams
- Lazy pulled streams
- Playlist files

Follow the instructions below on how to use WebRTC for streaming:



## WebRTC Streaming

1. To play streams from EMS using webRTC, the `startWebrtc` command needs to be executed first. See `startWebRTC`API [here](api_startWebRTC.html):

   ```
   startwebrtc ersip=54.174.188.145 ersport=4545 roomid=MyRoom
   ```

   **Note:** The room name should be **unique** as much as possible, especially when using the public ERS to prevent room name conflicts. If the room name is already taken, EMS would return an error on the console logs to indicate such scenario.

   ​

2. Access the test page `demo/evoplayers.html`

   ```
   http://<WEBSERVER_IP_ADDRESS>/demo/evoplayers.html
   ```

3. Enter the **EMS IP**, **Room Name** and **Stream Name** 

   **Note:** The Stream Name can be a pulled stream, a lazypulled file or a playlist file. Lazy pull and playlist files should be in the media folder.

   ​

4. Hit **Play** to start streaming!

   ​

   **Playing RTMP/RTSP Pulled Streams:**

   ![](images/html5/webrtc.jpg)

   ​

   **Playing Lazy Pulled File:**

   ![](images/html5/play_wrtc_lazypull.jpg)

   ​

   **Playing Playlist File:**

   ![](images/html5/play_wrtc_playlist.jpg)




**Note:**

There are two players available for WebRTC. You can stream the same source or stream two different sources at the same time!



## WebRTC using SRTP

This player uses SRTP as transport instead of fragmented MP4. To stream using this player, just follow the same steps as above but use the WebRTC SRTP player. 

![](images/html5/play_wrtcsrtp.jpg)



**Note:** 

- In case your stream audio is not working, it means that the browser does not support WebRTC AAC





## WebRTC ERS connections using SSL

Connections to ERS, from the client (browser) and server (EMS), can now also use SSL to prevent any sniffing of the traffic. To enable SSL connections:

1. On the ERS, modify the following in default.json configuration file

   ```
   "secure": true,
   "key": "/path/to/server.key",
   "cert": "/path/to/server.cert"
   ```

2. In EMS, add `ersOverSsl` parameter in webrtc in config.lua

   ```
   webrtc={
   		ersOverSsl=true,                              --> Add parameter
   		sslKey="/path/to/server.key",
   		sslCert="/path/to/server.cert",
   	   },
   ```

3. In the JS player, modify this value in the "opts" object that is used to configure the player

   ```
   ersOverSsl: true
   ```

4. Restart EMS and start streaming!

------

## Related Links

- [Starting WebRTC](api/startWebRTC.html)
- [Stopping WebRTC](stopWebRTC.html)

