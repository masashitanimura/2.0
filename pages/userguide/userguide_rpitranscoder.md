---
title: Raspberry Pi OMX-based Transcoder
sidebar: userguide_sidebar
permalink: userguide_rpitranscoder.html
folder: userguide
toc: false
---

EMS 2.0 Raspberry Piパッケージでは、Open Maxトランスコーダー(OMXTX)を使用したトランスコードができます。これはRaspberry Piパッケージのみで、対応するストリーム仕様は以下の通りです。


- Codec: h264/aac
- 最大入出力解像度: 1080p
- Transport: rtmp
- フォーマット: flv



## 手順

### ビデオのりサイズ

下記のコマンドはストリームの解像度を変更します


```
/path_to/rpitx -r 640x480 rtmp://<hostip:hostport>/live/<localstreamname> rtmp://<hostip:hostport>/live/out.flv
```



### オーディオの無効化

ストリームからオーディオを削除します

**書式:**

```
/path_to/rpitx -s noaudio rtmp://<hostip:hostport>/live/cam rtmp://<hostip:hostport>/live/noaudio.flv
```



**Note:**

- `listStreams`コマンドでトランスコードされたストリームを確認できます
