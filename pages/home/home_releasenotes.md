---
title: Release Notes
keywords: release notes
sidebar: home_sidebar
permalink: /home_releasenotes.html
folder: home
toc: false
---

# EMS 2.0.1

## Notable Bug Fixes

- Removed Google and Facebook account login options on the UI login page to prevent unauthorized access
- Fixed an issue where you were unable to play VOD files using aliasing in Windows
- Restricted API’s used by angular for better UI security
- Fixed playback of RTMP streams when the EMS is running in daemon clustered mode
- Fixed playback in Edge where buffer clearing (which is used to maintain low latency) caused playback skipping
- Minor UI improvements such as fixing API names in API explorer and corrected port number entry in dashboard





# EMS 2.0.0

## Highlights

- HEVC/H.265 support - HLS and DASH playback
- New Web UI - Node.js based with full access to EMS API
- New Evo-Webserver based on Node.js
- IPv6 support for all protocols
- Integration ready player libraries for Browsers, iOS and Android
- Direct playback via `<video>` tag, no player required!
- New Raspberry-Pi hardware-enabled transcoder


------

## New Features

- Android/iOS Peer to peer (WebRTC) playback now uses SRTP
- HTML5 Events for easy integration of Browser Player
- Rewritten example webservices into Javascript
- Server-Side-Playlist support for WebRTC and Websocket/HTML playback
- Lazy-Pull support for WebRTC and Websocket/HTML playback
- TCP TURN now available for WebRTC connections
- TLS encrypted ERS Communications for browser and EMS connections
- Support for COTURN and other compatible STUN/TURN servers
- Metadata delivery over websockets


------

## New APIs

- addMetadataListener - adding metadata listeners on the fly
- listMetadataListeners - list these metadata ingestion points
- getInboundStreamsCount - a more precise method versus GetStreamsCount
- getLicenseId - to programatically retrieve your license id. used by the new UI


------

## New Events

- hdsChunkClosed
- hlsChunkClosed
- dashChunkClosed
- webRtcServiceStarted
- webRtcServiceStopped


------

## Notable Bug Fixes

- Log files will now roll appropriately including between runs of the EMS
- HTTP-Proxy now properly uses "?" instead of "%3f" to separate the parameters from the URL
- Major improvements to Websocket and WebRTC browser player
- Proper retry of ERS connection if a disconnect occurs
- Added an RTSP buffer variable in config.lua to prevent trimming of very large key-frames
- Fixed FUA issue on outbound RTP/RTSP streams
- fixed random stream name on MPEG-TS push
- Fixed infrequent audio/video sync issue on DASH
- Fixed processing of playlistname and chunkbasename parameters for createHLSstream command
- Fixed to allow audio/video only HLS
- Fixed an issue in the mp4writer where it would choke on very large files