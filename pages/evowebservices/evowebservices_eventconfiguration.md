---
title: Configuring EMS Event Notifications
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_eventconfiguration.html
folder: evowebservices
toc: false
---

EMS Event Notifications must be configured to communicate with the EMS Web Services. The EMS configuration file must be modified as follows. Please view the [Configuring Event Notification](userguide_eventsoverview.html#configuring-event-notificationl) for more detailed information on configuring Event Notifications.



**config.lua:**

```
eventLogger= 
{
  sinks=
  { 
    {
      type="RPC", 
      url="http://127.0.0.1:4000/evowebservices/",
      serializerType="JSON",
      enabledEvents= 
      { 
		"inStreamCreated",
		"inStreamClosed",
		"outStreamCreated",
		"outStreamClosed",
		"timerTriggered",
		"hdsMasterPlaylistUpdated",
		"hdsChildPlaylistUpdated",
		"hdsChunkClosed",
		"hdsChunkDeleted",
		"hlsMasterPlaylistUpdated",
		"hlsChunkClosed",
		"hlsChunkDeleted",
		"dashPlaylistUpdated",
		"dashChunkClosed",
		"dashChunkDeleted",
      }, 
    }, 
  }, 
}, 
```

The **enabledEvents** parameter allows you to specify only the events which you wish to receive.It is highly recommended **not to add or delete** in the list. The listed events are those that the node webservices are using. If the event is missing, the service will not work. Additional events are ignored. 

The evowebservices rely on EMS Events being generated as follows:

- **RPC – Remote Procedure Calls**

  Event details are transmitted to a remote host via HTTP POST. The EMS will ignore any response from the remote host.

  RPC sink configuration:

  ```
  type="RPC",
  url="http://localhost:4000/evowebservices/",                    -- for node      (EMS v2.0.0)
  url="http://localhost/evowebservices/evowebservices.php",       -- for php		(EMS v1.7.1)
  serializerType="JSON" 
  ```

  The url field specifies the destination which will be accepting the HTTP POST event notifications. In this example, the web services are installed on the same computer that the EMS is running on (“localhost”). This value can be changed to the IP address of the computer running the web services.



- **serializerType**

  Format for the event logs. The serializerType can in the format of JSON, XML or XMLRPC.

  Sample format of JSON:

  ```
  {"payload":{"creationTimestamp":1349335053486.4370,"name":"","queryTimestamp":1349335053487.4370,"type":"NR","uniqueId":1,"upTime":1.0000},"type":"streamCreated"}
  ```


------

## Related Links

- [Event Overview](userguide_eventsoverview.html)
- [Events List](userguide_eventslist.html)
- [Event Definition](userguide_eventsdefinition.htmll)