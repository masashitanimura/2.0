---
title: listConfig
keywords: api
sidebar: api_sidebar
permalink: listConfig.html
folder: api
toc: false
---



Returns a list with all push/pull configurations.

Whenever the `pullStream` or `pushStream` interfaces are called, a record containing the details of the pull or push is created in the pullpushconfig.xml file. Then, the next time the EMS is started, the pullpushconfig.xml file is read, and the EMS attempts to reconnect all of the previous pulled or pushed streams.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listConfig
```



### Success Response in JSON

``` 
{
"data":{
    "dash":[details of dash streams],
    "hds":[details of hds streams],
    "hls":[details of hls streams],
    "metalistener":[details of metalistener added],    
    "mss":[details of mss streams],
    "process":[details of on process commands sent],
    "pull":[details of pulled streams],
    "push":[details of pushed streams],
    "record":[details of recorded streams],
    "webrtc":[details of started webRTC channels]
    },
"description":"Run-time configuration",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - dash - the details of [`createDASHStream`](createDASHStream.html)
  - hds - the details of [`createHDSStream`](createHDSStream.html)
  - hls - the details of [`createHLSStream`](createHLSStream.html)
  - metalistener - the details of [addMetadataListener](addMetadataListener.html)
  - mss - the details of [`createMSSStream`](createMSSStream.html)
  - process - the details of process commands
  - pull - the details of  [`pullStream`](pullStream.html)
  - push - the details of [`pushStream`](pushStream.html)
  - record - the details of [`record`](record.html)
  - webrtc - the details of [`startWebrtc`](startWebRTC.html)


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- Only the configurations with a `keepAlive` value of **true** will be listed
- Active configurations will also be listed

------

## Related Links

- [removeConfig](removeConfig.html)
- [getConfigInfo](getConfigInfo.html)