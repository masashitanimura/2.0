---
title: Pull a Stream
keywords: pullstream
sidebar: userguide_sidebar
permalink: userguide_pullstream.html
folder: userguide
toc: true
---

EMSはストリームプロトコルの再カプセル化を行う堅牢なプラットフォームを提供します。つまりひとつのストリーミングプロトコルから他のストリーミングプロトコルへ変換を行うことができるため、元のvideo/audioに設定が特定のクライエント向けのものであっても、多様なクライエント向けにアクセスを可能とします。

プロトコルの再カプセル化を行う第一歩はEMSに元となるストリームを取り込むことから始まります。最も頻繁につかわれるのは“**Pull**”ストリームによる方法です。外部のシステムからEMSのストリームをプッシュすることも可能です。



`pullStream` APIにより、EMSが既存ストリームを取得してくるように指示します



## 手順

下記の例のようにストリームをプルします:

### RTMP ストリーム

```
pullStream uri=rtmp://<STREAM_ADDRESS> localStreamName=RTMPTest
```



### RTSP ストリーム

```
pullStream uri=rtsp://<STREAM_ADDRESS> localStreamName=RTSPTest
```



### RTP - UDP ストリーム

```
pullStream uri=rtp://<STREAM_ADDRESS> localStreamName=RTPTest isAudio=0 spsBytes=Z0LAHpZiA2P8vCAAAAMAIAAABgHixck= ppsBytes=aMuMsg==
```



### MPEG-TS ストリーム

#### UDP MPEG-TS ストリーム

```
pullStream uri=dmpegtsudp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest
```

マルチキャストストリームでも使用できます。IPマルチキャスト範囲内のアドレスであればEMSは自動的にマルチキャストグループにjoinし、ストリームをプルします。


#### TCP MPEG-TS

```
pullStream uri=dmpegtstcp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest
```

**Note:**

mpegtsの前に付くの “**d**”は ( **d**mpegts) “deep parsing”を意味します。このURIをつかうことでインバウンドMPEG-TSストリームをRTMPやRTSPなどのプロトコルに再カプセル化するこができます。出力フォーマットがMPEG-TSのみ(EMSをMPEG-TS pass-throughとして使う)の場合は、mpegtsudpおよび mpegtstcpをURIプロトコル指定に使用できます。この場合パースの必要がないのでMPEG-TSストリームの転送処理が高速になります。



### LOCAL SDPファイル

EMSはSession Description Protocol (SDP)をプルすることが可能です。SDPはストリーミングメディアセッションの初期化パラメータの記述フォーマットです。SDPはメディアそのものの配信は行わず、エンドポイント間でのメディアタイプやフォーマットその他のプロパティのネゴシエーションに使用されます。


```
pullStream uri=file://<FILEPATH>/FILENAME.sdp localStreamName=sdpFileTest
```

**Note:**
SDPはEMSがアクセスできるファイルシステム上になければなりません。




## JSON CLI レスポンス

**API コール:**

```
pullstream uri=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 localStreamname=testpullstream
```

**JSON レスポンス:**

```
Command entered successfully!
Stream rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 enqueued for p
ulling

    configId: 1
    forceTcp: false
    keepAlive: true
    localStreamName: testpullstream
    uri:
      fullUri: rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4
      port: 1935
      scheme: rtmp
```



## プルしたストリームの再生

EMSにストリームが追加されたら、さまざま方法でアクセスすることができます。EMSのストリーミングプロトコル変換機能により、ターゲットプレーヤーが使えるフォーマットでリクエストをするだけであとはEMSが適切に処理してくれます。


プルしたストリームの基本的な再生コマンドは以下のように行います:


- **RTMP**

  RTMP URIフォーマット:

  ```
  rtmp[t|s]://[username[:password]@]ip[:port]/<appName>/<stream_name>
  ```

  RTMPストリームを再生するには、下記のURIをFlashプレーヤで利用します:

  ```
  rtmp://<EMS_IP_ADDRESS>/live/localStreamName
  ```

- **RTSP**

  RTSP URIフォマット:

  ```
  rtsp://[username[:password]@]ip[:port]/[ts|vod|vodts]/<stream_name or MP4 file name>
  ```

  **Note:**

  "appName"フィールドが無いだけで、コマンドはRTMPにとても似ています。

  RTSPストリームを再生するには下記のURIをRTSP再生が可能なプレーヤで利用します。


  ```
  rtsp://<EMS_IP_ADDRESS>:5544/localStreamName
  ```

  EMSはデフォルトでvideo/audioペイロードをRTP経由で送ります。MPEG-TSにしたい場合は下記のURIを指定します:

  ```
  rtsp://<EMS_IP_ADDRESS>:5544/ts/localStreamName
  ```

------

## 関連リンク:

- [pullStream API](api_pullStream.html)
- [Adding Inbound Streams](userguide_add.html#adding-inbound-live-streams)
- [Stream AutoRouting Service](evowebservices_streamautorouting.html)
