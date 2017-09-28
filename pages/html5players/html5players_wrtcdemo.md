---
title: Playing Videos Using evoplayers.html
keywords: webrtc
sidebar: html5players_sidebar
permalink: html5players_wrtcdemo.html
folder: html5players
toc: false
---

Starting release 2.0, the HTML5 web player of EMS or what we've called the evoplayers, can now play different streams such as: pulled RTMP/RTSP streams, lazy pulled streams and playlist files. Follow the instructions below on how to use webRTC for streaming:



1. To play streams from EMS using webRTC, the `startWebrtc` command needs to be executed first. See `startWebRTC`API [here](api/startWebRTC.html):

   ```
   startwebrtc ersip=54.174.188.145 ersport=4545 roomid=MyRoom
   ```

   **Note:** The room name should be unique as much as possible, especially when using the public ERS to prevent room name conflicts. If the room name is already taken, EMS would return an error on the console logs to indicate such scenario.

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

------

## Related Links

- [Starting WebRTC](api/startWebRTC.html)
- [Stopping WebRTC](stopWebRTC.html)

