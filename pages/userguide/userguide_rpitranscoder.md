---
title: Raspberry Pi OMX-based Transcoder
sidebar: userguide_sidebar
permalink: userguide_rpitranscoder.html
folder: userguide
toc: false
---

EMS 2.0 Raspberry Pi package is now capable of transcoding with the use of Open MAX transcoder (OMXTX).  Note that this is for Raspberry Pi package only.  Below are the accepted stream specifications:

- Codec: h264/aac
- Max input/output resolution: 1080p
- Transport: rtmp
- Format: flv



## How To

### Resizing Video

This command will change the width and height of your stream.

```
/path_to/rpitx -r 640x480 rtmp://<hostip:hostport>/live/<localstreamname> rtmp://<hostip:hostport>/live/out.flv
```



### Disable Audio

This will remove the audio of your stream.

**Format:**

```
/path_to/rpitx -s noaudio rtmp://<hostip:hostport>/live/cam rtmp://<hostip:hostport>/live/noaudio.flv
```



**Note:**

- Send `listStreams` to check the transcoded streams