---
title: Browser Compatibility
keywords: websocket
sidebar: html5players_sidebar
permalink: emscloud_wscompatibility.html
simple_map: false
map_name: usermap
box_number: 1
folder: emscloud
---



##  

The following diagram shows the compatibility of various browsers with the EvoStream WebSocket feature. 

![](images/emscloud/proto2.png)



**Firefox Configuration Changes**

The following configuration changes must be made to Firefox before it will work with HTML5 playback and Peer to Peer:

- In the Firefox address field enter: about:config
  - Click “I’ll be careful I promise!”
- Locate the following variables and set them (double-click) as necessary to match:
  - media.mediasource.enabled = true
  - media.mediasource.whitelist = false
  - media.mediasource.mp4.enabled = true
  - media.fragmented-mp4.exposed = true
  - media.fragmented-mp4.ffmpeg.enabled = true
  - media.fragmented-mp4.gmp.enabled = true
  - media.fragmented-mp4.use-blank-decoder = false
- Restart Firefox to activate these changes

