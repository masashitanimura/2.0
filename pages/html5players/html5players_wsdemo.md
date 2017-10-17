---
title: Playing Videos Using WebSockets
keywords: websocket
sidebar: html5players_sidebar
permalink: html5players_wsdemo.html
folder: html5players
toc: true
---

Starting release 2.0, the HTML5 web player of EMS or what we've called the evoplayers, can now play different streams such as: pulled RTMP/RTSP streams, lazy pulled streams and playlist files. Follow the instructions below on how to use WebSocket for streaming:



## WebSocket Streaming

1.  Access the test page `demo/evoplayers.html`

   ```
   http://<WEBSERVER_IP_ADDRESS>/demo/evoplayers.html
   ```

2. Enter the EMS IP address and the stream name of the stream/lazy pull file/playlist file you want to play

   **Note:** Lazy pull and playlsit files should be in media folder

   ​

3. Enter the EMS IP address and the stream name of the stream you want to play. 

4. Hit **Play** to start streaming!

   **Playing RTMP/RTSP Pulled Streams:**

   ![](images/html5/websocket.JPG)

   ​

   **Playing Lazy Pulled File:**

   ![](images/html5/play_ws_lazypull.jpg)

   ​

    **Playing Playlist File:**

   ![](images/html5/play_ws_playlist.jpg)

   ​

   **Note:**

   There are two players available for WebSocket. You can stream the same source or stream two different sources at the same time!






## WebSocket Over SSL

This WebSocket player uses an encrypted transport (SSL) to secure the websocket connection. To stream using this:

1. Enable WebSockets over SSL FMP4 Fetch in config.lua

   ```
   -- WebSockets over SSL FMP4 Fetch
   				--[[                                           ---- remove comments to enable
   				{
   					ip="0.0.0.0",
   					port=8420,
   					protocol="inboundWSSFMP4",
   					sslKey="C:\\EvoStream\\config\\server.key",
   					sslCert="C:\\EvoStream\\config\\server.cert",
   				},
   				]]--                                           ---- remove comments to enable
   ```

2. Modify the parameters if needed

3. Restart EMS

4. Access the test page `demo/evoplayers.html` and you can now stream using the WebSocket Over SSL player!

   ![](images/html5/play_wsssl.jpg)

   ​

**Notes:**

- We encourage to use a signed certificate for this

- If you will use a self-signed certificate, add the certificate to the exception/trusted publishers of the browser before using the player

  ​

