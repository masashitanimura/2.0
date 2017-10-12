---
title: Using API Proxy Authentication
keywords: apiproxy
sidebar: userguide_sidebar
permalink: userguide_usingapiproxy.html
folder: userguide
toc: true
---

Starting EMS v.2.0, the apiProxy is already enabled by default. You can see the configuration in the [webconfig.json](userguide_webconfig.html#apiproxy):

```
"apiProxy": 
	{
		"enable" : true,
		"authentication": "basic", 			
		"pseudoDomain": "apiproxy",
		"address": "127.0.0.1",
		"port": 7777,
		"userName": "username",
		"password": "password"
	}
```

Proxy authentication provides a way to secure the HTTP based EMS API. All API commands will first pass through the EWS, which will validate the provided **username** and **password**, and then pass the commands to the EMS for processing. API command return values will be routed back to the caller appropriately.



## How To Send API Commands using Proxy Authentication

API calls using Proxy Authentication will be formatted as follows:

```
http://userName:password@EMS_IP:EWS_PORT/pseudoDomain/command?params=([base64 encoded parameters])
```

**Note:** The EWS_PORT above is defined in webconfig.json under applications > rootDirectory > port. The EWS in EMS uses port 8888.



**Command without Parameters:**

```
http://username:password@localhost:8888/apiproxy/version
```

**Command Result:**

![](images/userguide/proxyone.jpg)





**Command with Parameters:**

You need to encode the parameters to base64 format. You can use any online tools available for encoding. Place the encoded parameters in the URL next to "param=".

```
http://username:password@localhost:8888/apiproxy/pullstream?params=dXJpPQlydG1wOi8vczJwY2h6eG10eW1uMmsuY2xvdWRmcm9udC5uZXQvY2Z4L3N0L21wNDpzaW50ZWwubXA0IGxvY2Fsc3RyZWFtbmFtZT1teVN0cmVhbQ==
```



**Command Result:**

![](images/userguide/proxytwo.jpg)



**Note:** 

- The browser has a JSON Parser extension
- If you will not place the username and password in URL, the browser will prompt for a username and password