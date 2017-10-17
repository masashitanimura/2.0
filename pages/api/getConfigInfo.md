---
title: getConfigInfo
keywords: api
sidebar: api_sidebar
permalink: getConfigInfo.html
folder: api
toc: false
---



Returns the information of the stream by the configId.



## API Parameter Table



| Parameter Name |  Type   | Mandatory | Default Value | Description                              |
| :------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|       id       | integer |   true    |    *null*     | The `configId` of the configuration to get some information |

## API Call Template

``` 
getConfigInfo id=<configId>
```



### Sample API Call

``` 
getConfigInfo id=1
```



### Success Response in JSON

``` 
{
          "data": {
                    "data": {
                              "appName": "evostreamms",
                              "audio": {
                                        "aveAudioBitRate": 99782.9887,
                                        "bytesCount": 6674408,
                                        "codec": "AAAC",
                                        "codecNumeric": 4702111241970123000,
                                        "currAudioBitRate": 97521.6,
                                        "droppedBytesCount": 0,
                                        "droppedPacketsCount": 0,
                                        "packetsCount": 25132
                              },
                              "bandwidth": 0,
                              "connectionType": 1,
                              "creationTimestamp": 1508229946197.202,
                              "farIp": "127.0.0.1",
                              "farPort": 1935,
                              "ip": "127.0.0.1",
                              "name": "bunny",
                              "nearIp": "127.0.0.1",
                              "nearPort": 5401,
                              "outStreamsUniqueIds": null,
                              "pageUrl": "",
                              "port": 5401,
                              "processId": 9468,
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
                                        "localStreamName": "bunny",
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
                              "queryTimestamp": 1508230481106.7979,
                              "serverAgent": "FMS/3,0,1,123",
                              "swfUrl": "rtmp://localhost/vod/bunny.mp4",
                              "tcUrl": "rtmp://localhost/vod/bunny.mp4",
                              "type": "INR",
                              "typeNumeric": 5282249572905648000,
                              "uniqueId": 66,
                              "upTime": 534909.5959,
                              "video": {
                                        "aveFrameRate": 24.0547,
                                        "aveKeyFramesPerSec": 0.3528,
                                        "aveVideoBitRate": 416097.9472,
                                        "bytesCount": 27987536,
                                        "codec": "VH264",
                                        "codecNumeric": 6217274493967008000,
                                        "currFrameRate": 24,
                                        "currKeyFramesPerSec": 0.2,
                                        "currVideoBitRate": 397163.2,
                                        "droppedBytesCount": 0,
                                        "droppedPacketsCount": 0,
                                        "height": 240,
                                        "level": 30,
                                        "packetsCount": 12871,
                                        "profile": 66,
                                        "width": 424
                              }
                    },
                    "description": "Stream information",
                    "status": "SUCCESS"
          }
}
```



#### JSON Response

The JSON response contains the following details:

- data – The information about the configuration
  - Other fields present are dependent on stream type


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- The response varies depending on the configuration.


------

## Related Links

- [listConfig](listConfig.html)
- [removeConfig](removeConfig.html)