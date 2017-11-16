---
title: Overview
keywords: api
sidebar: api_sidebar
permalink: api_overview.html
folder: api
toc: false
---

This document describes the Application Programming Interface (API) and Event Notification Systems presented by the EvoStream Media Server (EMS).

The EMS provides a bi-directional RESTful API for interacting with it both manually and programmatically. It allows you to write simple web services and scripts to extend and build your own logic on top of the EMS.

The API is composed of two parts. The calls you can make into the EMS is our **API**. The second part is the **Event Notification System** which calls you back when stuff happens with the EMS.

The API provides the ability to manipulate the server at runtime. The server can be told to retrieve or create new streams, return information on streams and connections, or even start or stop functional services.  The [Event Notification System](eventsoverview.html) provides a means for the EMS to alert users of certain events that occur within the EMS, such as a new stream is created, a stream has been dropped, server stopped, etc. 

Using these two halves of the API you can perform complex load balancing, create custom stream work flows, encrypt and protect your stream traffic and more, all on the fly, and with simple and efficient web services or local scripts.

EvoStream provides a set of sample web services that leverage the API. These web services can be found on our website and can be used directly or leveraged to start your own project. Download them [here](https://evostream.com/software-downloads/).