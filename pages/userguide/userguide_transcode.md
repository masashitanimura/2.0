---
title: Transcode Streams
keywords: transcode
sidebar: userguide_sidebar
permalink: userguide_transcode.html
folder: userguide
toc: true
---

EMSはさまざまな機能をもつソフトウェアエンコーダーもパッケージの中に持っており、LibAVのAVConvエンコーダーが選択されています。AVConvのソースコードは[http://libav.org/download.html](http://libav.org/download.html)から取得できます。EvoStreamはGPLに基づいてAVConvをコンパイルおよび配布しています。

**EMSは異なるソフトウェアエンコーダーを使うように設定でき、スクリプトによりオンデマンド変更することができます**

トランスコードはビデオやオーディオの圧縮に非常に多くのオプションが絡む複雑なプロセスですが、EMSでは`transcode` APIコールひとつですべてのプロセスを実行できます。


**Note:**

トランスコードには大きなコンピュータリソースを必要とするプロセスで、パフォーマンスに大きな影響を及ぼします。保守的なガイドラインとしては一つのHDストリームの処理にCPUコアひとつが必要です。



## 手順

### ストリームのビットレート変換

トランスコードのよくあるケースとして、Adaptive Streamingプロトコルをサポートしたり、AndroidやiOSデバイス向けの対応のためのHDストリームの低いビットレートへの“translating”(ダウンスケーリング)があります。

EMSにオリジナルのHDストリームを入力し、次のようなコマンドで複数の低ビットレートストリームを生成することができます。


**フォーマット:**

```
transcode source=rtmp://<stream_source> groupName=<groupName> videoBitrates=<bitrate> destinations=<destinationName>
```

**サンプルAPIコール:**

```
transcode source=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 groupName=group1 videoBitrates=100k,200k,300k destinations=stream100,stream200,stream300
```

**JSON レスポンス:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- na
      -- na
      -- na
    croppings:
      -- na
      -- na
      -- na
    destinations:
      -- stream100
      -- stream200
      -- stream300
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: stream300
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName:
    source: rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- stream100
      -- stream200
      -- stream300
    videoBitrates:
      -- 100k
      -- 200k
      -- 300k
    videoSizes:
      -- na
      -- na
      -- na
```

上記コマンドは **Source1**ストリームから３つの新規ストリームを生成します。**stream100**は100kbps、**stream200**は200kbps、**stream300**は300kbpsのビットレートです。`listStreams`コマンドで生成されたストリームを確認できます。

これらのストリームに直接アクセス（RTMPやRTSPで）したり、HLSグループを生成しiOSデバイス向けのadaptive bitrateストリームをつくることができます。


**トランスコードしたストリームからHLSを生成する:**

```
createhlsstream localstreamnames=stream100,stream200,stream300 targetfolder=/mywebroot/hls groupname=MyGroup playlisttype=rolling playlistLength=10 chunkLength=20
```



### 別コーデックに変換

EMSは通常H.264/AACを必要としますが、ストリームソースがこれ以外の場合にEMS Transcoderを用いてH.264/AACに変換することができます:


**フォーマット:**

```
transcode source=<stream_source>/localStreamName groupName=<groupName> videoBitrates=<bitrate> audioBitrates=<bitrate> destinations=<destinationName>
```

**サンプルAPIコール:**

```
transcode source=rtsp://IpOfStreamSource:554/myStream groupName=group1 videoBitrates=5000k audioBitrates=800k destinations=myTranscodedStream
```

**JSON レスポンス:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- 800k
    croppings:
      -- na
    destinations:
      -- myTranscodedStream
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: myTranscodedStream
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName:
    source: rtsp://127.0.0.1:5544/myStream
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- myTranscodedStream
    videoBitrates:
      -- 5000k
    videoSizes:
      -- na
```

上記コマンドはソースストリームをRTSPソースから直接プルし、トランスコードして`destinationName`に送り込みます。`videoBitrates`パラメータは必須設定パラメータです。`audioBitrates`パラメータはオーディオのトランスコードが必要な場合は必須設定パラメータです。オーディオもビデオもトランスコードの必要が無い場合はこれらのパラメータは無視されます。ソースストリームはビデオビットレート5Mbps、オーディオビットレート800kbpsが想定されています。




### ファイルを入出力に使用する:

入力ストリームをファイルに出力、またはファイル入力をファイル出力とする手順です

**フォーマット:**

```
transcode source=file://path_to_sourceFile groupName=group videoBitrates=<bitrate> audioBitrates=<bitrate> destinations=file://path_to_outputFile
```

**サンプルAPIコール:**

```
transcode source=file://C:\EvoStream\media\bunny.mp4 groupName=group1 videoBitrates=100k audioBitrates=copy destinations=file://C:\EvoStream\media\transcoded.mp4 keepAlive=0
```

**JSON レスポンス:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- copy
    croppings:
      -- na
    destinations:
      -- file://C:\EvoStream\media\transcoded.mp4
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName:
    fullBinaryPath: C:\EvoStream\emsTranscoder.bat
    groupName: group1
    keepAlive: false
    localStreamName:
    source: file://C:\EvoStream\media\bunny.mp4
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- na
    videoBitrates:
      -- 100k
    videoSizes:
      -- na
```



### ビデオオーバーレイ - 透かし(Watermarking)

EMS Transcoderはビデオオーバーレイを生成することができます。アルファ付きのPNGやJPEGファイルを用意する必要があります。
 **静止画はビデオと同一解像度かそれ以下のものを用意する必要があります**。オーバーレイは左上隅を起点として配置されます。
 オーバーレイを生成するには以下のコマンドで行います:



**フォーマット:**

```
transcode source=<localStreamName> groupName=<groupName> overlays0=<path/to/image.ext> destinations=destinationName
```

**サンプルAPIコール:**

```
transcode source=myStream groupName=group1 overlays=/path/to/evologo.jpg destinations=OverlayedStream
```

**JSON レスポンス:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- na
    croppings:
      -- na
    destinations:
      -- OverlayedStream
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: OverlayedStream
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName: myStream
    source: stream100
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- OverlayedStream
    videoBitrates:
      -- na
    videoSizes:
      -- na
```



### クロップ

EMS Transcoderはビデオクロッピングに対応しています。

**フォーマット:**

```
transcode source=<localStreamName> groupName=<groupName> croppings=<horizontalPosition:verticalPosition:width:height> destinations=destinationName
```

**サンプル API:**

```
transcode source=myStream groupName=group1 croppings=0:0:50:50 destinations=CroppedStream
```

**JSON レスポンス:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- na
    croppings:
      -- 0:0:50:50
    destinations:
      -- CroppedStream
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: CroppedStream
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName: myStream
    source: myStream
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- CroppedStream
    videoBitrates:
      -- na
    videoSizes:
      -- na

```

上記は右上起点で50px X 50pxの正方形にビデオがクロップされます。`croppings`パラメータの書式はhorizontalPosition:verticalPosition:width:heightで表され、horizontalPosition=0は左端ピクセルを意味し、verticalPosition=0は上端ピクセルを意味します



### インバウンドRTSPにTCPを強制する

```
transcode source=rtmp://<RTMP server>/live/streamname groupName=group videoBitrates=copy videoSizes=360x200 $EMS_RTSP_TRANSPORT=tcp
```



## トランスコードプロセスを中止する

`removeconfig` APIを実行しトランスコードを中止できます

**フォーマット:**

```
removeConfig groupName=<groupName>
```

**サンプルAPIコール:**

```
removeConfig groupName=group1
```

**JSON レスポンス:**

```
Command entered successfully!
Configuration terminated
```

**group1**内のすべてのトランスコードプロセスが削除されます



## Transcode Logsの有効化

`transcode` コマンドはemsTranscoder.shを呼び出します。トランスコード関連の問題の原因を追求するには以下の手順でログを有効化してください:

1. コメントを外し`transcode`ログを有効化する

   **ウインドウズでは: emsTranscoder.bat**

   ```
   rem echo %TRANSCODER_BIN% %TRANSCODE%   //remove rem
   ```

   **Linuxでは: emsTranscoder.sh**

   ```
   #echo "$TRANSCODER_BIN $TRANSCODE"     //remove #
   ```

2. EMSコンソールで, `transcode`コマンドを実行し、evo-avconvコマンド実行状況を確認します


3. evo-avconv 実行結果をコピーします

   **サンプル log:**

   ```
   evo-avconv -y -i rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 -b:v 100K -c:v libx264 -c:a copy -metadata streamName=testTransDest rtmp://192.168.2.35/live/testTransDest
   ```

4. evo-avconv実行結果を新規コンソールでペーストします  (locate in evo-avconv executable)

   **サンプル log:**

   ```
   C:\EvoStream>evo-avconv -y -i rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 -b:v 10
   0K -c:v libx264 -c:a copy -metadata streamName=testTransDest rtmp://192.168.2.35/live/testTransDest
   avconv version 11.3, Copyright (c) 2000-2014 the Libav developers
     built on Jul 15 2015 10:16:52 with gcc 4.8 (GCC)
   [flv @ 0000000000302da0] max_analyze_duration 5000000 reached
   Input #0, flv, from 'rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4':
     Metadata:
       moovPosition    : 40
       avcprofile      : 66
       avclevel        : 30
       aacaot          : 2
       videoframerate  : 24
       audiochannels   : 2
       ┬⌐too           : Lavf52.84.0
       length          : 2293760
       timescale       : 44100
       sampletype      : mp4a
     Duration: 00:00:52.20, start: 0.000000, bitrate: N/A
       Stream #0.0: Video: h264 (Constrained Baseline), yuv420p, 720x306 [PAR 254:255 DAR 2032:867], 24
    fps, 1k tbn, 48 tbc
       Stream #0.1: Audio: aac, 44100 Hz, stereo, fltp
   Unable to find a suitable output format for 'rtmp://192.168.2.35/live/testTransDest'
   ```
