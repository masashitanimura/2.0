---
title: Push a Stream
keywords: pushstream
sidebar: userguide_sidebar
permalink: userguide_pushstream.html
folder: userguide
toc: true
---

ソースストリームによってストリームをプッシュする手順は異なります。


## プッシュの手順

それぞれのフォーマットについてストリームをプッシュする手順の例を以下に記述します stream in different formats:

### RTMP ストリーム

```
pushStream uri=rtmp://DestinationAddress localStreamName=SomeLocalStreamName
```



### RTSP ストリーム

```
pushStream uri=rtsp://DestinationAddress:port localStreamName=SomeLocalStreamName
```



### MPEG-TS ストリーム

MPEG-TS ストリームには一般的にストリームid(名前)の概念がありません。EMSは内部用にインバウンドMPEG-TSに名前を割り当てますが、外部ではこの名前は使用されません。MPEG-TSストリームをEMSから取得するにはEMSからネットワークにプッシュされる必要があります。

コマンド例を以下に示します:

```
pushStream uri=mpegtsudp://DestinationAddr localStreamName=SomeLocalStream
```

または

```
pushStream uri=mpegtstcp://DestinationAddr localStreamName=SomeStream
```




## JSON CLI レスポンス

**API Call:**

```
pushStream uri=rtmp://192.168.2.105/live localStreamName=testpullstream targetStreamName=testpushstream
```

**JSON レスポンス:**

```
Command entered successfully!
Local stream testpullstream enqueued for pushing to rtmp://192.168.2.105/live as
 testpushstream

    configId: 2
    forceTcp: false
    keepAlive: true
    localStreamName: testpullstream
    targetStreamName: testpushstream
    targetStreamType: live
    targetUri:
      fullUri: rtmp://192.168.2.105/live
      port: 1935
      scheme: rtmp
```



## プッシュされたストリームの再生

プッシュされたストリームの再生はプルされたストリームの再生と似ています

EMSにプッシュされたストリームを再生する基本コマンド:

- **RTMP**

  RTMP URIフォーマット:

  ```
  rtmp[t|s]://[username[:password]@]ip[:port]/<appName>/<stream_name>
  ```

  RTMPストリームの再生をFlashプレーヤー行うには下記のURIを使用します:

  ```
  rtmp://<EMS_IP_ADDRESS>/live/localStreamName
  ```

- **RTMP**

  RTSP URIフォーマットでは次のようになります:

  ```
  rtsp://[username[:password]@]ip[:port]/[ts|vod|vodts]/<stream_name or MP4 file name>
  ```

  **Note:**

  コマンドは"appName"フィールドが無いことを除きRTMPと同じです

  RTSPストリームをRTSP再生可能なプレーヤーで再生するには下記のようなURIを使います。

  ```
  rtsp://<EMS_IP_ADDRESS>:5544/localStreamName
  ```

  EMSはデフォルトでvideo/audioペイロードデータをRTP経由で送ります。MPEG-TSにしたい場合はリクエストURIで指定してください：

------

## 関連リンク:

- [pushStream API](api_pushStream.html)
- [Send Stream To Facebook](userguide_send.html#facebook-live)
- [Send Stream To Youtube](userguide_send.html#youtube-live)
- [Stream Load Balancer Service](evowebservices_streamloadbalancer.html)
