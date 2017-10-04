---
title: EMS Stream Types
keywords: stream
sidebar: userguide_sidebar
permalink: userguide_streamtypes.html
folder: userguide
toc: false
---

The stream type is found on the stream details. Whenever you call the `listStreams`, you will see type along with the stream details. Below are the different stream types for reference:

| Stream Type                       | Description                              |
| --------------------------------- | ---------------------------------------- |
| INR (Inbound Network RTMP)        | an RTMP stream coming in from the network into the EMS |
| INLFLV (Inbound Network Live FLV) | a Live FLV stream is coming in from network into EMS |
| INTS (Inbound Network TS)         | a TS stream is coming in from network into EMS |
| INP (Inbound Network RTP)         | a RTP stream is coming in from network into EMS |
| IFR (Inbound File RTMP)           | a RTMP file is coming in from network into EMS |
| IFT (Inbound FIle TS)             | a TS file is coming in from network into EMS |
| IFP (Inbound File RTSP)           | a RTSP file is coming in from network into EMS |
| ONFMP4 (Outbound Network FMP4)    | a FMP4 stream is coming out from EMS     |
| ONMP4 (Outbound Network MP4)      | an MP4 stream is coming out from EMS     |
| ONR (Outbound Network RTMP)       | a RTMP stream is coming out from EMS     |
| ONP  (Outbound Network RTP)       | a RTP stream is coming out from EMS      |
| ONTS (Outbound Network TS)        | a TS stream is coming out from EMS       |
| OFR (Outbound File RTMP)          | an RTMP file is coming out from EMS      |
| OFHLS (Outbound File HLS)         | a HLS stream is coming out from EMS      |
| OFHDS (Outbound File HDS)         | a HDS stream is coming out from EMS      |
| OFMSS (Outbound File MSS)         | a MSS stream is coming out from EMS      |
| OFDASH (Outbound File DASH)       | a DASH stream is coming out from EMS     |
| OFTS (Outbound File TS)           | a TS file is coming out from EMS         |
| OFMP4 (Outbound File MP4)         | an MP4 file is coming out from EMS       |

**Notes:**

- char 1 = I for inbound, O for outbound
- char 2 = N for network, F for file
- char 3+ = further details about stream