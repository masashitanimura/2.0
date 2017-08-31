---
title: Video On Demand
keyword: vod
sidebar: userguide_sidebar
permalink: userguide_videoondemand.html
folder: userguide
toc: false
---

The first critical step to getting Video on Demand (VOD) working is to place all of the media files into the appropriate directory. By default that directory is the `media` folder in the main EMS folder. If a different folder is to be used for the media files, simply modify the `config.lua` file and change the `mediaFolder` parameter with the new path.

```
			mediaStorage={
				recordedStreamsStorage="C:\\EvoStream\\media",
				{
					description="Default media storage",
					mediaFolder="C:\\EvoStream\\media",
				},
```

See [mediaStorage](userguide_configlua.html#mediastorage) for more details.



## VOD - RTMP

VOD to RTMP is handled automatically by EMS, simply provide the target player with the appropriate URI.

For Example:

```
rtmp://<SERVER_ADDRESS>/vod/NameOfFile.ext
```

The only trick is in the name of the file. The URI needs to be formatted depending on the file type. The following rules will need to be followed:

**Supported File Types:**

| File Type | Streaming URI Value                      |
| --------- | ---------------------------------------- |
| *.flv     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.flv |
| *.mp4     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.mp4 |
| *.mov     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.mov |
| *.m4v     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.m4v |

It is also possible to have the media files in subdirectories of the main media file:

```
rtmp://<SERVER_ADDRESS>/vod/mp4:subFolder1/subFolder2/NameOfFile.ext
```

The EMS dynamically generates “**Seek**” and “**Meta**” which allow the client to “click around” in the video and play from any time-point in the video. Please note that if the original video file on the server is moved, the Seek and Meta files cannot be moved along with it. They use absolute file paths and must be deleted so that they can be regenerated for the video file again.



## VOD - RTSP with RTP or MPEG-TS

VOD to RTSP is also handled automatically by the EMS, simply provide the target player with the appropriate URI.

For Example:

```
rtsp://<SERVER_ADDRESS>:5544/vod/NameOfFile.ext
```

Since the FLV format is specifically designed for RTMP, **FLV file playback for RTSP is not supported**. Any MP4 file, however, can be played with RTSP. This simplifies the format for the VOD request:

**Supported File Types:**

| File Type | Streaming URI Value                      |
| --------- | ---------------------------------------- |
| *.flv     | *not supported*                          |
| *.mp4     | rtsp://< SERVER_ADDRESS >5544/vod/NameOfFile.mp4 |
| *.mov     | rtsp://< SERVER_ADDRESS >5544/vod/NameOfFile.mov |
| *.m4v     | rtsp://< SERVER_ADDRESS >5544/vod/NameOfFile.m4v |

It is also possible to have the media files in subdirectories of the main media file:

```
rtsp://<SERVER_ADDRESS>:5544/vod/mp4:subFolder1/subFolder2/NameOfFile.ext
```

By default, the EMS will send the video/audio payload data via RTP. If MPEG-TS is needed instead, simply specify it in the request URI:

```
rtsp://<SERVER_ADDRESS>:5544/vodts/video2.mov
```

The EMS dynamically generates “**Seek**” and “**Meta**” which allow the client to “click around” in the video and play from any time-point in the video. Please note that if the original video file on the server is moved, the Seek and Meta files cannot be moved along with it. They use absolute file paths and must be deleted so that they can be regenerated for the video file again.



## HLS VOD Work Around

HLS is not explicitly designed for traditional VOD. It is designed to take a live stream, convert it to small files, and then serve those files to iOS devices. iOS devices (such as iPhones and iPads) can already handle the download and play many audio and video files directly from online sources.

There is, however, a way to do VOD with HLS using the EMS. The trick is to create a live stream using RTMP first, and then use the new live stream for the HLS stream.

Following is an example set of commands:

```
Issue a pullStream command:
pullStream uri=rtmp://<SERVER_ADDRESS>/vod/video.mov keepAlive=1 localstreamname=DummyLive

Issue createHLSStream command:
createHLSStream localstreamnames=DummyLive bandwidths=128 targetfolder=../evo-webroot/ groupname=hls playlisttype=rolling playlistLength=10 chunkLength=20
```



## VOD Playback with Stream Aliases Enabled

Aliases can also be applied on VOD streams. Once the `hasStreamAliases` is enabled, you cannot play the file directly using the file name itself.

To do playback in VOD:

```
rtsp://<SERVER_ADDRESS>:5544/vod/<aliasname>
rtmp://<SERVER_ADDRESS>/vod/<aliasname>
```

