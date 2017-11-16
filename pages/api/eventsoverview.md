---
title: Events Overview
keyword: events
sidebar: api_sidebar
permalink: eventsoverview.html
folder: api
toc: true
---

The EMS Event Notification System provides an extremely powerful way of interacting with the EMS. At the basic level it allows you to easily understand and monitor the usage of your server. You can either poll and parse the log file, or simply subscribe to the HTTP based notifications sent out by the EMS. **The notifications mean that you can have a fully RESTful monitor, gathering metrics in real time!**



Beyond monitoring and gathering metrics, you can **use the Event Notification System to create custom stream processing.** If you want to automatically create HLS/HDS/MSS/DASH streams out of new inbound streams, simply call `createHLSStream` / `createHDSStream` / `createMSSStream` / `createDASHStream` in response to each “new inbound stream” event. If you want to close inbound streams when the associated outbound stream is lost, call `shutdownStream` when you receive an “outbound stream closed” event.



## Configuring Event Notification

Events can be sent to multiple destinations, or “sinks”, at the same time. A “sink” can be either a file or a network destination. Multiple sinks can be enabled at the same time, allowing you to both log events and receive them in your web service(s). These sinks can be configured so that only the events you will be consuming will be generated. Event Sinks are configured in the `config.lua` file.

```
eventLogger=
{
    sinks=
    {
        type="sink1_type",
        -- property1 of sink1
        -- property2 of sink1
    },
    enabledEvents=
    {
        "inStreamCreated",
        "inStreamClosed",
    }
},
```



### Sinks

Sinks are defined as “a specific destination for events” and can be of two types: “file” and “RPC” which are detailed below. 

For any Sink, users can define an array of *enabledEvents*. When this array is present, **only** the events listed will be sent to that sink. If this array is not present, **all** events will be sent to the sink. The full list of events can be found later in this document.



### Application vs. Server Events

The config.lua file has two eventLogger sections as follows:

1. Application-owned – This is lower in the file and is “inside” the application configuration section. It configures “application level” events. **This is the recommended configuration section to modify.**
2. Server-wide (or default) – This is higher in the file and is at the outer-most variable scope level. This section configures events that are outside the application or events which the application level fails to catch. This is typically only for system events like server startup, server shutdown and application load.



### Enabling Event Logs

Event Notifications are off by default. To use the Event Notification System, you must modify the EMS configuration file:

1.  Remove comment to the eventLogger section in the configuration `--[[ ]]--`
2.  Select your preferred filename and file format
3.  Configure time-stamp if to be used
4.  Select events that will be enabled under 








## Types of Event Sinks

There are two main types of event sinks, the **File Event Sink** and the **Remote Procedure Calls Event Sink**



### File Event Sink

File sinks simply write events to a file, as defined by the “filename” parameter. This works much like a system logger. Users can choose the format of the output between JSON, XML, W3C and text. The file sink is **off** by default, but can be turned on by creating the sink in the `config.lua` file.

**Note:** The log file is overwritten each time the EMS starts up.

```
type="file",
filename="log.txt",
format="text",
customData="my custom data"
```

**File sink configuration:**

The format can be one of the following types:

- “text” (plain text) - The Text format writes to the event file in a way that is easy to read, where events are on multiple lines

- “xml” - Each event files are written to a single line in XML format

- “json” - Each event files are written to a single line in JSON format

- “w3c” - The W3C formatted file is compliant with the requirement of having space or tab-delimited columns. In addition, it has a header line that is commented out (#) that indicates the names of the columns



A typical configuration of a file sink follows:

```
eventLogger=
  {
      sinks=
      {
          {
              type="file",
              filename="../logs/events.txt",
              --format="text",
              --format="xml",
              --format="json",
              format="w3c",
              timestamp=true,
              appendTimestamp=true,
              appendInstance=true,
              fileChunkLength=43200, -- 12 hours (in seconds)
              fileChunkTime="18:00:00",
              enabledEvents=
              {
                  "inStreamCreated",
                  "outStreamCreated",
                  "streamCreated",
                  -- content removed for clarity
              },
              {
                  -- content removed for clarity

              },
          },
      },
  },
```

**Note:** This is disable by default in config.lua. 



#### File Sink Structure Table

|       Key       |  Type   | Mandatory | Description                              |
| :-------------: | :-----: | :-------: | ---------------------------------------- |
|   customData    | object  |    no     | Custom data that will be appended to all events generated by this sink. It overrides the custom data node defined on the upper level. It can also be a complex structure, see illustration above. |
|      type       | string  |    yes    | The type of sink, “file”.                |
|    filename     | string  |    yes    | The base name of the file.               |
|     format      | string  |    yes    | Sets the file format. Allowed values are “text”, “xml”, “json” and “w3c” |
|    timestamp    | boolean |    no     | Adds timestamp to file                   |
| appendTimestamp | boolean |    no     | Sets the option to append a timestamp. If **true**, timestamp (YYYYMMDD_HHmmSS) is appended on every log file created. Otherwise, a 4-digit running number is appended. Default value is **true** |
| appendInstance  | boolean |    no     | Appends a random 4-digit instance ID after every log file. Default is false. |
| fileChunkLength | number  |    no     | Number of seconds to create new file.    |
|  fileChunkTime  | string  |    no     | Time of the day to chunk log file, in HH:MM:SS format. **Note:** No file chunking when `fileChunkLength` and `fileChunkTime` are both present. |
|  enabledEvents  | object  |    no     | Events that are logged. If not set, all are logged. But for W3C, non-stream-related events are ignored. |



As indicated above, the name of the file can be set using a number of options. For example,

```
filename = "/var/evostreamms/logs/streams"
appendTimestamp = true
appendInstance = true
```
The log file would be `/var/evostreamms/logs/streams_0237_20140311_183046.txt`.



### RPC (Remote Procedure Calls) Event Sink

To receive HTTP based Event Notifications, an RPC type sink must be defined (and is by default). The URL parameter defines the location that will be called with each event. The URL can be a specific web service script or just an IP and port on which service is listening to that can interpret these events. RPC sinks have the option of one of three serializer types, or in other words, the way the data will be formatted within the HTTP post: JSON, XML, XMLRPC

Event details are transmitted to a remote host via HTTP POST. The EMS will ignore any response from the remote host.

**RPC sink configuration:**

```
type="RPC",
url="http://192.168.1.5:5555/something/service",
serializerType="JSON",
customData="my custom data"
```

The `url` field specifies the destination which will be accepting the HTTP POST event notifications..

The `serializer` type can be one of the following formats:

- **JSON**

  The JSON serializer type has the same schema as XML, but is formatted as JSON.

  ```
  {"payload":{"creationTimestamp":1349335053486.4370,"name":"","queryTimestamp":1349335053487.4370,"type":"NR","uniqueId":1,"upTime":1.0000},"type":"streamCreated"}
  ```

- **XML**

  The XML serializer type uses an XML schema that is more condensed and specific to the EMS Event Notification System

  ```
  <?xml version="1.0" ?>
  <MAP isArray="false" name="">
      <MAP isArray="false" name="payload">
          <DOUBLE name="creationTimestamp">1349335287346.813</DOUBLE>
          <STR name="name"></STR>
          <DOUBLE name="queryTimestamp">1349335287346.813</DOUBLE>
          <STR name="type">NR</STR>
          <UINT64 name="uniqueId">1</UINT64>
          <DOUBLE name="upTime">0.000</DOUBLE>
      </MAP>
  <STR name="type">streamCreated</STR>
  </MAP>
  ```

- **XMLRPC**

  The XML format using a traditional XML-RPC schema

  ```
  <?xml version="1.0"?>
  <methodCall>
      <methodName>event.Log</methodName>
      <params>
          <param>
              <value>
                  <struct>
                      <member>
                          <name>payload</name>
                          <value>
                              <struct>
                              <member>
                                  <name>creationTimestamp</name>
                                  <value><double>0.000000</double></value>
                              </member>
                              <!-- contents removed for clarity -->
                              </struct>
                          </value>
                      </member>
                      <member>
                          <name>type</name>
                          <value><string>streamCreated</string></value>
                      </member>
                  </struct>
              </value>
          </param>
      </params>
  </methodCall>
  ```



The `customData` parameter for both File and RPC Event Sinks can be *optionally* used to extra data to each event for that sink. This could be used to identify the particular EMS instance which is generating the event, return a particular ID or Key which is pertinent to your handling of the event, or anything really! A `customData` parameter can be a simple sting value or a complex LUA object.

If a `customData` parameter is not specified for a node, the value of the parent `eventLogger` `customData` node will be used. If that is also not specified, the value will be V_NULL.

------

## Notes

- The event sinks should be enabled to be able to use events
- Event logs will be saved in the configured `filename` 
- You can add or remove events in list
- Only the events selected will be shown in the logs

------

## Related Links

- [List of Events](eventslist.html)

  ​