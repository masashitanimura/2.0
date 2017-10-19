---
title: listInboundStreams
keywords: api
sidebar: api_sidebar
permalink: listInboundStreams.html
folder: api
toc: false
---



Provides a complete detailed list of all the current inbound `localStreamNames`.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listInboundStreams
```



### Success Response in JSON

``` 
{
          "data": {
                    "data": [
                              {
                                        "appName": "evostreamms",
                                        "audio": {
                                                  "aveAudioBitRate": 102226.8169,
                                                  "bytesCount": 940870,
                                                  "codec": "AAAC",
                                                  "codecNumeric": 4702111241970123000,
                                                  "currAudioBitRate": 96889.6,
                                                  "droppedBytesCount": 0,
                                                  "droppedPacketsCount": 0,
                                                  "packetsCount": 3523
                                        },
                                        "bandwidth": 0,
                                        "connectionType": 1,
                                        "creationTimestamp": 1508320715972.891,
                                        "edgePid": 0,
                                        "farIp": "127.0.0.1",
                                        "farPort": 1935,
                                        "ip": "127.0.0.1",
                                        "name": "bunnyqwe",
                                        "nearIp": "127.0.0.1",
                                        "nearPort": 6448,
                                        "outStreamsUniqueIds": null,
                                        "pageUrl": "",
                                        "port": 6448,
                                        "processId": 612,
                                        "processType": "origin",
                                        "pullSettings": {
                                                  "_callback": null,
                                                  "audioCodecBytes": "",
                                                  "configId": 1,
                                                  "emulateUserAgent": "EvoStream Media Server (www.evostream.com) player",
                                                  "forceTcp": false,
                                                  "httpProxy": "",
                                                  "httpStreamType": "ts",
                                                  "isAudio": true,
                                                  "keepAlive": true,
                                                  "localStreamName": "bunnyqwe",
                                                  "operationType": 1,
                                                  "pageUrl": "",
                                                  "ppsBytes": "",
                                                  "rangeEnd": -1,
                                                  "rangeStart": -2,
                                                  "rtcpDetectionInterval": 10,
                                                  "saveToConfig": true,
                                                  "sendDummyPayload": false,
                                                  "sendRenewStream": false,
                                                  "spsBytes": "",
                                                  "ssmIp": "",
                                                  "swfUrl": "",
                                                  "tcUrl": "",
                                                  "tos": 256,
                                                  "ttl": 256,
                                                  "uri": "rtmp://localhost/vod/bunny.mp4",
                                                  "videoSourceIndex": "high"
                                        },
                                        "queryTimestamp": 1508320789466.095,
                                        "serverAgent": "FMS/3,0,1,123",
                                        "swfUrl": "rtmp://localhost/vod/bunny.mp4",
                                        "tcUrl": "rtmp://localhost/vod/bunny.mp4",
                                        "type": "INR",
                                        "typeNumeric": 5282249572905648000,
                                        "uniqueId": 56,
                                        "upTime": 73493.2039,
                                        "video": {
                                                  "aveFrameRate": 24.3944,
                                                  "aveKeyFramesPerSec": 0.3239,
                                                  "aveVideoBitRate": 395857.2394,
                                                  "bytesCount": 3605399,
                                                  "codec": "VH264",
                                                  "codecNumeric": 6217274493967008000,
                                                  "currFrameRate": 24,
                                                  "currKeyFramesPerSec": 0.6,
                                                  "currVideoBitRate": 259859.2,
                                                  "droppedBytesCount": 0,
                                                  "droppedPacketsCount": 0,
                                                  "height": 240,
                                                  "level": 30,
                                                  "packetsCount": 1806,
                                                  "profile": 66,
                                                  "width": 424
                                        }
                              },
                              {
                                        "appName": "evostreamms",
                                        "audio": {
                                                  "aveAudioBitRate": 0,
                                                  "bytesCount": 0,
                                                  "codec": "AAAC",
                                                  "codecNumeric": 4702111241970123000,
                                                  "currAudioBitRate": 0,
                                                  "droppedBytesCount": 0,
                                                  "droppedPacketsCount": 0,
                                                  "packetsCount": 0
                                        },
                                        "bandwidth": 512,
                                        "connectionType": 0,
                                        "creationTimestamp": 1508320715979.892,
                                        "edgePid": 0,
                                        "farIp": "127.0.0.1",
                                        "farPort": 6448,
                                        "ip": "127.0.0.1",
                                        "name": "C:\\EvoStream_2.0\\media\\bunny.mp4",
                                        "nearIp": "127.0.0.1",
                                        "nearPort": 1935,
                                        "outStreamsUniqueIds": [
                                                  57
                                        ],
                                        "port": 1935,
                                        "processId": 612,
                                        "processType": "origin",
                                        "queryTimestamp": 1508320789466.095,
                                        "type": "IFR",
                                        "typeNumeric": 5279997773091963000,
                                        "uniqueId": 58,
                                        "upTime": 73486.2029,
                                        "userAgent": "EvoStream Media Server (www.evostream.com) player",
                                        "video": {
                                                  "aveFrameRate": 0,
                                                  "aveKeyFramesPerSec": 0,
                                                  "aveVideoBitRate": 0,
                                                  "bytesCount": 0,
                                                  "codec": "VH264",
                                                  "codecNumeric": 6217274493967008000,
                                                  "currFrameRate": 0,
                                                  "currKeyFramesPerSec": 0,
                                                  "currVideoBitRate": 0,
                                                  "droppedBytesCount": 0,
                                                  "droppedPacketsCount": 0,
                                                  "height": 240,
                                                  "l,evel": 30,
                                                  "packetsCount": 0,
                                                  "profile": 66,
                                                  "width": 424
                                        }
                              },
                              {
                                        "appName": "evostreamms",
                                        "audio": {
                                                  "aveAudioBitRate": 124868.9032,
                                                  "bytesCount": 549716,
                                                  "codec": "AAAC",
                                                  "codecNumeric": 4702111241970123000,
                                                  "currAudioBitRate": 117090.6667,
                                                  "droppedBytesCount": 0,
                                                  "droppedPacketsCount": 0,
                                                  "packetsCount": 1686
                                        },
                                        "bandwidth": 0,
                                        "connectionType": 1,
                                        "creationTimestamp": 1508320754242.08,
                                        "edgePid": 0,
                                        "farIp": "204.246.165.52",
                                        "farPort": 1935,
                                        "ip": "192.168.2.193",
                                        "name": "testpullStream",
                                        "nearIp": "192.168.2.193",
                                        "nearPort": 6492,
                                        "outStreamsUniqueIds": null,
                                        "pageUrl": "",
                                        "port": 6492,
                                        "processId": 612,
                                        "processType": "origin",
                                        "pullSettings": {
                                                  "_callback": null,
                                                  "audioCodecBytes": "",
                                                  "configId": 3,
                                                  "emulateUserAgent": "EvoStream Media Server (www.evostream.com) player",
                                                  "forceTcp": false,
                                                  "httpProxy": "",
                                                  "httpStreamType": "ts",
                                                  "isAudio": true,
                                                  "keepAlive": true,
                                                  "localStreamName": "testpullStream",
                                                  "operationType": 1,
                                                  "pageUrl": "",
                                                  "ppsBytes": "",
                                                  "rangeEnd": -1,
                                                  "rangeStart": -2,
                                                  "rtcpDetectionInterval": 10,
                                                  "saveToConfig": true,
                                                  "sendDummyPayload": false,
                                                  "sendRenewStream": false,
                                                  "spsBytes": "",
                                                  "ssmIp": "",
                                                  "swfUrl": "",
                                                  "tcUrl": "",
                                                  "tos": 256,
                                                  "ttl": 256,
                                                  "uri": "rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4",
                                                  "videoSourceIndex": "high"
                                        },
                                        "queryTimestamp": 1508320789466.095,
                                        "serverAgent": "FMS/3,5,7,7009",
                                        "swfUrl": "rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4",
                                        "tcUrl": "rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4",
                                        "type": "INR",
                                        "typeNumeric": 5282249572905648000,
                                        "uniqueId": 59,
                                        "upTime": 35224.0149,
                                        "video": {
                                                  "aveFrameRate": 26.6774,
                                                  "aveKeyFramesPerSec": 0.4839,
                                                  "aveVideoBitRate": 1053309.6774,
                                                  "bytesCount": 4407924,
                                                  "codec": "VH264",
                                                  "codecNumeric": 6217274493967008000,
                                                  "currFrameRate": 25.3333,
                                                  "currKeyFramesPerSec": 0.3333,
                                                  "currVideoBitRate": 1299993.3333,
                                                  "droppedBytesCount": 0,
                                                  "droppedPacketsCount": 0,
                                                  "height": 306,
                                                  "level": 30,
                                                  "packetsCount": 940,
                                                  "profile": 66,
                                                  "width": 720
                                        }
                              }
                    ],
                    "description": "Available inbound streams",
                    "status": "SUCCESS"
          }
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.

  - appName - EvoStream Media Server

  - audio – stats about the audio portion of the stream

    - aveAudioBitRate - The average bitrate of the audio frames from the start of the stream
    - bytesCount - Total amount of audio data received
    - codec - The name of the audio codec 
    - codecNumeric - Code used for internal use only
    - currAudioBitRate - The bitrate of the last audio frame received when calling the command
    - droppedBytesCount - The number of video bytes lost
    - droppedPacketsCount – The number of lost audio packets
    - packetsCount – Total number of audio packets received

  - bandwidth – The current bandwidth utilization of the stream

  - connectionType - 1=pull, 2=push, 3=HLS, 4=HDS, 5=MSS, 6=DASH, 7=record, 8=launchprocess, 9=webrtc, 10=metadata, 0=standard

  - canDropFrames – *Outstreams only*. Flag set by client allowing for dropped frames/packets

  - creationTimestamp – The UNIX timestamp for when the stream was created. UNIX time is expressed as the number of seconds since the UNIX Epoch (Jan 1, 1970)

  - edgePid – Internal flag used for clustering

  - farIp - The IP address of the distant party

  - farPort - The port used by the distant party

  - ip - IP address of the source stream’s host

  - inStreamUniqueID – *For pushed streams.* The id of the source stream.

  - name – the `localStreamName` for this stream

  - nearIp - The IP address used by the local computer

  - nearPort - The port used by the local computer

  - outStreamsUniqueIDs – *For pulled streams.* An array of the “out” stream IDs associated with this “in” stream

  - pageUrl - A link to the page that originated the request (often unused)

  - port - The port bound to the service

  - processId - The process ID of the EMS instance processing the API command

  - processType - Origin or edge, depending on the EMS instance processing the API command

  - queryTimestamp – The time (in UNIX seconds) when the information in this request was populated

  - serverAgent - The server agent used

  - type – The type of stream this is. The first two characters are of most interest:

    - char 1 = I for inbound, O for outbound

    - char 2 = N for network, F for file

    - char 3+ = further details about stream

      example: INR = Inbound Network Stream (a stream coming from the network into the EMS)

  - typeNumeric - A number obtained from an array of 8 bytes filled with the characters of the stream type padded with 0's

  - uniqueId – The unique ID of the stream

  - uptime – The time in seconds that the stream has been alive/running for

  - userAgent -  The string that the EMS uses to identify itself with the other server. It can be modified so that EMS identifies itself as, say, a Flash Media Server

  - video – Stats about the video portion of the stream

    - aveFrameRate- The average frame rate since the stream has started
    - aveKeyFramesPerSec - The average keyframe per second since the stream has started
    - aveVideoBitRate -  The average bitrate of the video frames from the start of the stream
    - bytesCount - Total amount of video data received
    - codec - The name of the video codec 
    - codecNumeric - Code used for internal use only
    - currFrameRate - The number of video frames processed within a one second time frame
    - currKeyFramesPerSec - The number of video keyframes processed within a one second time frame
    - currVideoBitRate - The bitrate of the last video frame received when calling the command
    - droppedBytesCount – The number of video bytes lost
    - droppedPacketsCount – The number of lost video packets
    - height - The video stream’s pixel height
    - level - H264 level
    - packetsCount – Total number of video packets received
    - profile - H264 profile
    - width - The video stream’s pixel width

- description– Describes the result of parsing/executing the command

- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [listInboundStreamNames](listInboundStreamNames.html)