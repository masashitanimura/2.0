---
title: EMS Stream Types
keywords: stream
sidebar: userguide_sidebar
permalink: userguide_streamtypes.html
folder: userguide
toc: false
---

`listStreams`をコールするとストリームタイプおよびストリームの詳細情報が得られます。
下記は異なるストリームタイプとその内容です:


| ストリームタイプ                       | 内容                              |
| --------------------------------- | ---------------------------------------- |
| INR (Inbound Network RTMP)        | RTMPストリームがネットワークからEMSに入ってきている  |
| INLFLV (Inbound Network Live FLV) | Live FLVストリームがネットワークからEMSに入ってきている |
| INTS (Inbound Network TS)         | TS ストリームがネットワークからEMSに入ってきている |
| INP (Inbound Network RTP)         | RTP ストリーム がネットワークからEMSに入ってきている|
| IFR (Inbound File RTMP)           | RTMP ファイル がネットワークからEMSに入ってきている|
| IFT (Inbound FIle TS)             | TS ファイル がネットワークからEMSに入ってきている|
| IFP (Inbound File RTSP)           | RTSP ファイル がネットワークからEMSに入ってきている|
| ONFMP4 (Outbound Network FMP4)    | FMP4 ストリーム EMSから出力されている     |
| ONMP4 (Outbound Network MP4)      | MP4 ストリーム EMSから出力されている     |
| ONR (Outbound Network RTMP)       | RTMP ストリーム EMSから出力されている     |
| ONP  (Outbound Network RTP)       | RTP ストリーム EMSから出力されている      |
| ONTS (Outbound Network TS)        | TS ストリーム EMSから出力されている       |
| OFR (Outbound File RTMP)          | RTMP file EMSから出力されている      |
| OFHLS (Outbound File HLS)         | HLS ストリーム EMSから出力されている      |
| OFHDS (Outbound File HDS)         | HDS ストリーム EMSから出力されている      |
| OFMSS (Outbound File MSS)         | MSS ストリーム EMSから出力されている      |
| OFDASH (Outbound File DASH)       | DASH ストリーム EMSから出力されている     |
| OFTS (Outbound File TS)           | TS file EMSから出力されている         |
| OFMP4 (Outbound File MP4)         | MP4 file EMSから出力されている       |

**Notes:**

- char 1 = I がインバウンド、 O がアウトバウンド
- char 2 = N がネットワーク、F がファイル
- char 3+ = ストリームに関する詳細情報
