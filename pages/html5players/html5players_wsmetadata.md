---
title: WebSocket Metadata
keywords: websocket
sidebar: html5players_sidebar
permalink: html5players_wsmetadata.html
folder: html5players
toc: true
---

Metadata is data about data, or in this case, data about and/or related to streams. However, EMS offers ingest and delivery of these data that can virtually be anything: location data, images (like thumbnails), heart-rate data, etc. The current input format uses JSON but other forms can be added as needed. These metadata can then be sent to different players and/or another EMS endpoint.

Both Metadata Outbound Push and Metadata Ingest use a **Web Sockets Metadata Acceptor**. The EMS uses this to receive and/or send metadata.



## Ingestion and Aggregation

![](images/html5/capab1.png)



EMS accepts metadata, as well as live RTMP streams with metadata incorporated. EMS has two ways of accepting metadata: one is through a TCP acceptor, and the other is through websockets, which has been discussed in the HTML5 Web Sockets section.

The TCP and websockets acceptors are enabled by default but can be customized through the configuration file, config.lua.ua*):

```
acceptors =
{
    -- content removed for clarity
    -- JSONMETA
    {
	   ip="0.0.0.0",
	   port=8100,
	   --streamname="test",
	   protocol="inboundJsonMeta",
    },
    -- WebSockets JSON Metadata
    {
        ip="0.0.0.0",
        port=8210,
        protocol="wsJsonMeta",
        -- streamname="~0~0~0~"
    },
    -- WebSockets JSON Metadata over SSL
    {
       ip="0.0.0.0",
	  port=8433,
	  protocol="wssJsonMeta",
	  -- streamname="~0~0~0~"
	  sslKey="C:\\EvoStream\\config\\server.key",
	  sslCert="C:\\EvoStream\\config\\server.cert",
    },
    -- content removed for clarity
},
```

**Where:**

​	ip - the IP where the service is located. A value of 0.0.0.0 means all interfaces and all IPs

​	port - port number that the service will listen to

​	protocol - the protocol stack handled by the ip:port combination

​	streamname - the streamname where the metadata will be sent. if disabled, will match to all incoming streams

​	sslKey- the path to the ssl key to be used

​	sslCert - the path to the ssl certificate to be used



On the configuration above, the `streamname` parameter is optional, default will match **all** incoming streams.

Once a metadata is received, the EMS Metadata Manager stores these metadata and also incorporates them to the corresponding RTMP stream for outbound if needed.



## Metadata Delivery

![](images/html5/capab2.png)



EMS offers two mechanisms to send out the metadata it currently have. The first, is to have the clients manually query and poll EMS for the metadata. This is done through the following command:



**Get Metadata:**

```
getMetadata localStreamName=test
```

This command will return the corresponding metadata related to the stream "_test_".



**Push Metadata:**

The second mechanism is to send out metadata updates through a TCP connection. This assumes that the other endpoint would be able to parse the incoming metadata in JSON format. This mechanism is enabled through the following command:

```
pushMetadata localStreamName=test ip=192.168.2.1 port=8110
```

This will push updated metadata to a server which has an IP address of _192.168.2.1_ and is able to listen to incoming traffic on port _8110_.

The third mechanism of delivering metadata is through websockets. Any clients connected to the metadata websocket acceptor would be able to, not only send out metadata to EMS, but also receive metadata updates from EMS as well.

See [getMetadata](api_getMetadata.html) and [pushMetadata](api_pushMetadata.html) APIs.



```
ws://host:port/streamname
```

Use the GET format to open a websocket channel:

The `streamname` above, if not empty, will override what is specified in the acceptor definition in config.lua.

Matching JSON metadata arrives as text. Use WS.send() to input JSON metadata.

Below is a sample minimal metadata page:

```
<script>
    var ws= new WebSocket("ws://myems:8210/");
    ws.onmessage= function (msg) {
        console.log(msg.data);
    }
    Function doSend() {
        var x={fred:{wife:"Wilma",friend:"Barney"}};
        ws.send(JSON.stringify(x));
    }
</script>
<button onclick="doSend();">SEND</button>
```


For the FMP4 Player, a Web Sockets acceptor is defined in `config.lua`:

```
acceptors =
{
    -- content removed for clarity
    -- WebSockets FMP4 Fetch
    {
        ip="0.0.0.0",
        port=8410,
        protocol="inboundWSFMP4",
    },
    -- content removed for clarity
},
```

The above defines an outbound FMP4 acceptor. It does say “inbound” because the Web Socket connector is inbound, it being an acceptor.

```
ws://host:port/streamname

```

To connect, a Web Socket “GET” call is used. Following is the “GET” URI format

The *streamname* is a local stream name of a stream that is pulled in the EMS.

A sample HTML file with an FMP4 player, `evowsvideo.html`, is provided. You may use this to try out the Web Socket FMP4 functionality.

For convenience, a demo page is already available upon installation: `..\evo-webroot\demo\evoplayers.html` Another option for playback is using the [public evoplayer](ers.evostream.com:5050/demov2/evoplayers.html).

