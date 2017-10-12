---
title: Websockets Metadata Read and Write Demo Page
keywords: websocket
sidebar: html5players_sidebar
permalink: html5players_wsmetademo.html
folder: html5players
toc: true
---

A demo page for reading and sending metadata is available in ..evo-webroot/demo/. 



## jsonMetaWriteTest.html

This demo page allow you to send metadata in the stream using some stream configuration



1.  Access the test page `demo/jsonMetaWriteTest.html`

   ```
   http://<EMS_IP>:<WebserverPort>/demo/jsonMetaWriteTest.html
   http://127.0.0.1:8888/demo/jsonMetaWriteTest.html
   ```

2. Enter **Host**, **Port** and **Stream** you want to connect to:

   ![](images/html5/wsdemo_write.JPG)

   ​

   **Note:** The stream ~0 ~ 0 ~ 0 ~ means it will write to all stream names

   ​

3. Click **Connect**

   ![](images/html5/wsdemo_connected.JPG)

   ​

4. Change details in the stream configuration then click **Send**

   ![](images/html5/wsdemo_send.JPG)

   ​

   ​


## jsonMetaTest.html

This demo page reads the metadata in your stream.



1. Access the test page `demo/jsonMetaTest.html`

   ```
   http://<EMS_IP>:<WebserverPort>/demo/jsonMetaTest.html
   http://127.0.0.1:8888/demo/jsonMetaTest.html
   ```

   ​

2. Enter **Host**, **Port** and **Stream** you want to connect to:

   ![](images/html5/wsdemo_write.JPG)

   ​

   **Note:** The stream ~0 ~ 0 ~ 0 ~ means it will read the metadata in all stream names

   ​

3. Click **Connect**

   ![](images/html5/wsdemo_connected.JPG)

   ​

4. The metadata sent to the stream name will be shown in the page:

   ![](images/html5/wsdemo_read.JPG)



**Note:**

 The jsonMetaTest page should be opened prior in sending the metadata. It will not show the metadata sent before the page is opened. 