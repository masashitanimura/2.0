---
title: WebRTC Overview
keywords: webrtc
sidebar: html5players_sidebar
permalink: html5players_wrtcoverview.html
folder: emscloud
toc: false
---



The web real-time communications or much known as the **WebRTC** is a free, open project that provides browsers and mobile applications with Real-Time Communications (RTC) capabilities via simple APIs. 

It is a very exciting, powerful, and highly disruptive cutting-edge technology and standard.  **WebRTC** leverages a set of plugin-free APIs that can be **used** in both desktop and mobile browsers, and is progressively becoming supported by all major modern browser vendors. 

The **WebRTC** initiative is a project supported by Google, Mozilla and Opera, amongst others.



## Peer to Peer

The EMS supports direct peering to HTML5 browsers and devices that support WebRTC. Over the WebRTC channel, the EMS streams low-latency (sub-second) H.264 video and AAC audio for delivery directly to the HTML5 video player.

By moving the streaming directly between the end client and the stream originator (for example, a security camera) you remove the largest cost driver of hosting any kind of live streaming service: the bandwidth cost!

![](images/html5/proto1.png)



Peer to peer works when the _EMS is installed and running on the camera, wearable or other such stream creation device_. Here is the simplified work flow for Peer to Peer:

1. The EMS is configured to communicate with an **EvoStream Rendezvous Server** (ERS). The EMS will maintain that connection to the ERS while it waits for a peer request. The configuration specifies a unique "Room" in which it is waiting.

2. A WebRTC enabled browser/app will connect to a Web Server (either the one provided by the ERS or one of your choosing) and downloads a player page, including the EvoStream provided JavaScript Peering Code.

3. The browser loads the JavaScript, which has been pre-configured by the Web Server with 

   - an IP address of the ERS to connect to
   - a "Room" to connect to

4. The browser connects to the ERS and requests to join the "Room"

5. The EMS (on the camera) and the Browser share peering information across the ERS connection.

6. Using the peering information, the peer connection is established directly between EMS and the Browser and streaming proceeds.

   ​

EvoStream provides a hosted EvoStream Rendezvous Server at **52.6.14.61:4545**. Click [here](ers.evostream.com:5050/demov2/evoplayers.html) for the player. This server can be used for testing and for deployment. This can be used with the EMS by issuing the following API command:

```
startWebRTC ersIP=52.6.14.61 ersPort=3535 roomID=YourRoom
```

**It is VERY IMPORTANT TO NOTE:**

- This is a public ERS, and so many people may be using it
- If your RoomID is not unique, it will result in race conditions with other users. You may end up seeing their streams or they may see yours!
- EvoStream intends to make this ERS available at all times, but its uptime is NOT Guaranteed!

For production deployments of Peer To Peer you will want to host your own ERS, or have EvoStream host a separate ERS on your behalf. Please contact EvoStream for more information.



