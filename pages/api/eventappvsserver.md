---
title: Application vs. Server Events
keywords: events
sidebar: api_sidebar
permalink: eventappvsserver.html
folder: api
toc: false
---



## Application vs. Server Events

The config.lua file has two eventLogger sections as follows:

1. Application-owned – This is lower in the file and is “inside” the application configuration section. It configures “application level” events. **This is the recommended configuration section to modify.**

   ​

2. Server-wide (or default) – This is higher in the file and is at the outer-most variable scope level. This section configures events that are outside the application or events which the application level fails to catch. This is typically only for system events like server startup, server shutdown and application load.