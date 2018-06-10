---
title: Protocol Support and Specifics
keywords: API
sidebar: userguide_sidebar
permalink: userguide_protocols.html
folder: userguide
toc: true
---



本章はEvoStream Media serverの機能の詳細について記述されています。本文書でインバウンドやアウトバウンドとった方向性に関する言葉が出てくる際は常にEMSの観点からの方向性です。したがってインバウンドとはEMSに入ってくることを意味し、アウトバウンドはEMSから外に出ていくことを意味します。




## Real Time Messaging Protocol (RTMP)

EMSはRTMPプロトコルに完全に互換性があります。つまりEMSはAdobe Flash Media Live Encoder (FMLE)、Wirecast、Flash Applet等からのストリームを受信できます。またEMSからのストリームはFlowPlayer、JWPlayer、VLCといったAdobe-Airベースのクライエントで再生可能です。RTMPを使用するとFlashが使用できるWebブラウザがストリーム受信できる（ウインドウズ、Mac OS、Linux）ことになります。




### RTMPインジェスト

RTMPをストリームソースとしてEMSが使うには複数のやり方がありますが、ランタイムAPIを使用してソースストリームをプルする方法の例は以下のとおりです:

```
pullstream uri=rtmp://192.168.1.5/live/MyTestStream localStreamName=TestStream
```

上記コマンドは**192.168.1.5**のサーバーから**MyTestStream**を取得し、ローカル名**TestStream**とするようEMSに命令します。
ローカル名についてくわしくは[`pullStream` API](pullStream.html)をご覧ください。

RTMPストリームをリクエストするURI書式は:

```
rtmp://[username[:password]@]IP[:port]/<appName>/<localStreamName>
```



### アウトバウンド RTMP (Live ＆ VOD)

ソースストリームはRTMP経由で再生することができますが、EMSでRTMPリクエストによくつかわれるのはFlashベースのプレーヤーソフトです。
RTMPSストリームのリクエストは下記のURI書式を使用してください:


```
rtmp://[username[:password]@]IP[:port]/<live/vod>/<localStreamName>
```

URIサンプル:

```
rtmp://192.168.1.5/live/MyTestStream

```

EMSは他のサーバー等にストリームをプッシュすることもできます。`pushStream`ランタイムAPIが使用されます
`pushStream` APIの例:

```
pushStream uri=rtmp://192.168.1.5/live/ localStreamName=MyTestStream targetStreamName=PushedStreamName
```



### RTMPT

RTMP via HTTPをEMSはサポートしています。RTMPTはRTMPと同様に利用できます。URIで"RTMP"とするところを"RTMPT"と変えるだけです。
RTMPTクライエントからのリクエストにEMSを対応させるにはconfig.luaファイルで以下のようにAcceptor(listner)を作成する必要があります。


```
{
      ip="0.0.0.0",                                  
      port=8081,                                     
      protocol="inboundRtmpt"
},

```



### RTMPS


RTMP secured by SSLをEMSはサポートしています。RTMPSはRTMPと同様に利用できます。URIで"RTMP"とするところを"RTMPS"と変えるだけです。
RTMPSストリームを配信するには証明書とキーの作成と指定が必要になります。

OpenSSL(*.crt)などのライブラリをつかって署名付き証明書および対応するパブリックキー(*.pem)ファイルを作成する必要があります。
またconfig.luaファイルで次のようなAcceptor(listner)を作成する必要があります。


```
{
      ip="0.0.0.0",                                  
      port=8082,                                     
      protocol="inboundRtmps",                       
      sslKey="server.key",                           
      sslCert="server.crt"                           
},

```

上記の例ではsslKeyのパスはランタイムディレクトリからの相対パス表記ですが、絶対パスで記述した方が良いです。


上記のような設定はあくまでもこうしたファイルを配信する(RTMPSストリームリクエストを受ける)際にのみ必要であって、ストリームをプルしたりプッシュする場合には使われません。その場合は外部サーバーが自身のキーをつかって認証を行います。



### RTMP Ingest Points

Ingest Pointがアクティブな場合、EMSにプッシュされるストリームがTarget Stream Nameを持つ必要があります。信頼されたパートナーからEMSサーバーへのストリームプッシュを容易にしてくれます。

Ingest Pointは**privateStreamName** と **publicStreamName**の２つの関連する設定値を指定することにより運用されます。**privateStreamName** と **publicStreamName**はEMSインスタンスごとにユニークな値である必要があります。RTMPストリームがEMSにプッシュされる際、RTMPストリーム内で定義されたTarget Stream NameはprivateStreamNamesでの定義と一致させる必要があります。一致するとストリームはEMSにより受信されます。関連するpublicStreamNameを参照してEMSからこのストリームにアクセス可能です。

Ingest Pointを有効化するにはconfig.luaで`hasIngestPoints`パラメータをtrueに変更してください。


```
hasingestpoints=true,

```

Ingest Pointの追加や削除を行うフルセットのAPI関数があります。詳しくは[API Definition document](api_overview.html)をご参照ください

- [createIngestPoint](createIngestPoint.html)
- [removeIngestPoint](removeIngestPoint.html)
- [listIngestPoints](listIngestPoints.html)

Ingest Pointは**config/ingestPoints.xml**ファイルに保存されます [ingstpoints.xml](userguide_ingestpoints.html)



## Real Time Streaming Protocol (RTSP)

RTSPプロトコルはAndroid メディアプレーヤーを含むさまざまなプレーヤーやサーバーで使用できます。RTSPはストリームソースおよびアウトバウンドストリームプロトコルとして使用できます。RTSPにはいくつかのバリエーションがありプロトコルそのものについて多少の知識は必要です。

RTSPそのものはネゴシエーションプロトコルで、ビデオやオーディオの転送を扱うための接続をコーディネートし構築します。RTSP転送では4つのチャンネル - オーディオ、ビデオの他に、オーディオ／ビデオの同期用のReal Time Control Protocol(RTCP)接続が２チャンネルが作成されます。一般的にはRTSPストリームでは5つの異なる接続／ストリームが関係しています。

この他、オーディオとビデオストリームは、Real-time Transfer Protocol(RTP)またはMPEG Transport Stream(MPEG-TS)といったことなるメカニズム上で転送が可能です。EMSはRTSP over RTP/MPEG-TSのどちらにも対応しており、RTCP有り／なしにも対応しています。

通常RTCPチャンネルはRTSPストリームに含まれていますが、必須ではありません。EMSでもしかりなのですが、EMSでは新規RTSPストリームが入ってきた際に、RTCPチャンネルを検出するまで一定時間待ちます。この間はRTSPストリームのすべてのパケットがdropされます。待ち時間はconfig.luaのrtcpDetectionIntervalを編集することで調整できます。


### RTSPのインジェスト

EMSがストリームソースとしてRTSPを使用するにはいくつかのやり方がありますが、最初の方法はランタイムAPIによりストリームをプルすることです。
`pullstream`コマンドの例:


```
pullstream uri=rtsp://192.168.1.5/MyTestStream localStreamName=TestStream
```

上記のコマンドはEMSに**MyTestStream**を**192.168.1.5**のサーバーに取得しにいくよう命令し、ローカルで**TestStream**と命名します。
詳しくは [`pullStream` API](pullStream.html)をご参照ください

RTSPストリームリクエストの一般的なURI書式は以下です:

```
rtsp://[username[:password]@]IP[:port]/<stream or sdp file name>
```

HTTP proxy経由でRTSPストリームをプルするには`pullstream`コマンドを以下のように実行します:

```
pullstream uri=rtsp://[username[:password]@]HostName/StreamName httpProxy=IP[:PORT] localStreamName=TestStream
```

HTTP経由でRTSPストリームをプルする場合httpProxyパラメータを利用することができます:

```
pullstream uri=rtsp://[username[:password]@]HostName/StreamName httpProxy=self localStreamName=TestStream
```

**Note:**

`httpProxy=self`パラメータはproxyがないということを意味し、指定したURIから直接HTTP経由でストリームをプルします。

EMSにRTSPプッシュすることもできます。EMSはRTSPストリームを5544ポートで受けています（RTSPのデフォルトポートは554）。EMSにむけてRTSPをプッシュする際はポート5544を指定する必要があります。ポートはconfig.luaファイルを編集することによって変更が可能です。

EMSにストリームをプッシュする場合に認証と必要とするよう設定できます。認証が有効化されると、ストリームプッシュの際認証情報のやりとりが必要となります。詳しくは [authentication](userguide_aliasingandauthentication.html)をご覧ください。




### アウトバウンド RTSP (Live/VOD)

RTSP経由でソースストリームを再生することができます。よく使われるRTSPプレーヤーはVLC、Android Devices、 Quicktimeなどです。RTSPストリームをリクエストするには以下のようなURI書式をつかいます:


```
rtsp://[username[:password]@]IP[:port]/[ts|vod|vodts]/<LocalStreamName or MP4 file name>

```

RTSPリクエストのサンプル:

ライブRTSP/RTP ストリームのリクエスト:

```
rtsp://192.168.1.5:5544/MyTestStream

```

ライブRTSP/MPEG-TS ストリームリクエスト:

```
rtsp://192.168.1.5:5544/ts/MyTestStream

```

RTSP/RTP経由のVOD MP4ファイルのリクエスト:

```
rtsp://192.168.1.5:5544/vod/MyMP4File.mp4

```

RTSP/MPEG-TS経由のVOD MP4ファイルリクエスト:

```
rtsp://192.168.1.5:5544/vodts/MyMP4File.mp4

```

VODリクエストでは、ファイル名はメディアフォルダからの相対パスを含めることができます:

```
rtsp://192.168.1.5:5544/vod/folder1/folder2/MyMP4File.mp4

```

RTSP VOD再生ではMP4ファイルのみ使用できます。TSやFLVファイルはソースとして使用できません


EMSは他のサーバーへストリームをプッシュすることも可能です。この場合`pushStream`ランタイムAPI関数を使います。
 `pushStream` APIの例:

```
pushStream uri=rtsp://192.168.1.5:5544 localStreamName=MyTestStream targetStreamName=PushedStreamName
```



## MPEG Transport Stream (MPEG-TS)

EMSはUDP/TCP両方でMPEG2 Transport Streamをサポートします。UDP MPEG-TSストリームはユニキャスト・ブロードキャスト・マルチキャストを行えます。UDPマルチキャストストリームを受信するには、 **dmpegtsudp://**プロトコルインジケータ("d"はdeep-parseを意味します)をつかってpullstreamコマンドを実行する必要があります。


```
pullstream uri=dmpegtsudp://229.0.0.1:5555 localstreamname=TestTSMulticast

```

上記の書式で“**udp”**を“**tcp”**に変えるだけで、**TCP MPEG-TS**ストリームをプルすることができます:

```
pullstream uri=dmpegtstcp://192.168.1.5:5555 localstreamname=TestTSMulticast

```

**MPEG-TS TCP** ストリームはサーバーにプッシュすることもできますが、事前に**config.lua**で"acceptor"を作りどのポートでlistenするかを設定しておく必要があります:

```
{
	ip="0.0.0.0",
	port=9998,
	protocol="inboundTcpTs"
},
{
	ip="0.0.0.0",
	port=9999,
	protocol="inboundUdpTs"
},
```

上記のacceptor設定で、acceptorにプッシュするストリームの名前をあらかじめ設定しておける“localstreamname”変数を定義しておくことが可能です。こうすることで、acceptorが受信するインバウンドストリームをひとつに限定することができます。


下記の書式でMPEG-TSストリームがport9998にTCP経由でプッシュされた場合に“test1”という名前でストリームを生成します:
 `{ ip="0.0.0.0", port=9998, localstreamname="test1",protocol="inboundTcpTs" },`

config.luaファイルに変更を行った後、変更を適用するためにはEMSを再起動する必要があります。




## HTML5 Web Sockets

HTML5 Web Socketテクノロジーは、従来のようにサーバーがクライエントにデータを送信するためにクライエント側からリクエストを送り、サーバーがレスポンスを返すというHTTP requiest/responseモデルではなく、webブラウザとサーバーの間でソケット接続を提供する技術です。低レイテンシーアプリケーションではHTTPは多大なオーバーヘッドがあります。

Web Socketをつかえばクライエント（webブラウザ）／サーバー間での途切れがない接続を確率でき、双方どちらからいつでもデータを送信できます。クライエント側からリクエストを始めなければならないという制限がありません。より"リアルタイム"なデータ配信ができる低レイテンシー接続ができます。


EMSはこの技術をつかって次のような機能性を実現しています

- Metadata アウトバウンドプッシュ – ブラウザにメタデータを転送する
- Metadata インジェスト – incomingメタデータを受信.
- FMP4 Player – フラグメントMP4(FMP4)ストリームを配信するacceptor

くわしくは [詳細](html5players_wsoverview.html) をご参照ください



## プロトコル対応プレーヤー

次の図にはEvoStream 2.0がサポートするプロトコルについての対応プレーヤーがまとめられています。


![](images/userguide/protocolsupport_h264.JPG)



![](images/html5/ws_compatibility.JPG)



![](images/html5/webrtc_compatibility.JPG)
