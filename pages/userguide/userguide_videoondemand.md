---
title: Video On Demand
keyword: vod
sidebar: userguide_sidebar
permalink: userguide_videoondemand.html
folder: userguide
toc: false
---

ビデオオンデマンド(VOD)を動作させる際に重要なポイントはすべてのメディアファイルを適切なディレクトリ下に配置することです。デフォルトではEMSフォルダ下の`media`フォルダに設定されています。もし異なるフォルダを設定したい場合は、`config.lua`ファイルの`mediaFolder`パラメータを修正してください。

```
			mediaStorage={
				recordedStreamsStorage="C:\\EvoStream\\media",
				{
					description="Default media storage",
					mediaFolder="C:\\EvoStream\\media",
				},
```

詳しくは [mediaStorage](userguide_configlua.html#mediastorage) をご参照ください



## VOD - RTMP

EMSは自動的にRTMPでVODを行ってくれます。ターゲットプレーヤーと適切なURIを指定するだけです。

例:

```
rtmp://<SERVER_ADDRESS>/vod/NameOfFile.ext
```

ファイル名（拡張子）の部分を注意する必要があります。URIはファイルタイプによって次のような書式となります:


**対応ファイルタイプ:**

| ファイルタイプ | ストリーミング URI                    |
| --------- | ---------------------------------------- |
| *.flv     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.flv |
| *.mp4     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.mp4 |
| *.mov     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.mov |
| *.m4v     | rtmp://< SERVER_ADDRESS >/vod/NameOfFile.m4v |

メディアファイルはサブフォルダにあっても構いません:

```
rtmp://<SERVER_ADDRESS>/vod/mp4:subFolder1/subFolder2/NameOfFile.ext
```

EMSはダイナミックに“**シーク情報**” および “**メタデータ**”を生成し、ビデオの時系列上のどこからでも再生できるようにします。
サーバー上のファイル位置を変えた場合、シーク情報やメタデータも一緒に移動はしてくれません。これらは絶対パスを利用していますので、手動で削除し、再生成されるように仕向ける必要があります。



## VOD - RTP または MPEG-TSのRTSP

EMSは自動的にRTSPでVODを行ってくれます。ターゲットプレーヤーと適切なURIを指定するだけです。


例:

```
rtsp://<SERVER_ADDRESS>:5544/vod/NameOfFile.ext
```

FLVフォーマットはRTMP用なので、**RTSPでのFLVの再生はサポートされていません**。一方MP4ファイルはRTSPでの再生ができます:

**対応ファイルタイプ:**

| ファイルタイプ | ストリーミング URI                       |
| --------- | ---------------------------------------- |
| *.flv     | *not supported*                          |
| *.mp4     | rtsp://< SERVER_ADDRESS >5544/vod/NameOfFile.mp4 |
| *.mov     | rtsp://< SERVER_ADDRESS >5544/vod/NameOfFile.mov |
| *.m4v     | rtsp://< SERVER_ADDRESS >5544/vod/NameOfFile.m4v |

メディアファイルはサブフォルダにあっても構いません:

```
rtsp://<SERVER_ADDRESS>:5544/vod/mp4:subFolder1/subFolder2/NameOfFile.ext
```

EMSはデフォルトでビデオ／オーディオペイロードデータをRTP経由で送ります。MPEG-TSの場合は下記のURIを使用してくだだい:


```
rtsp://<SERVER_ADDRESS>:5544/vodts/video2.mov
```

EMSはダイナミックに“**シーク情報**” および “**メタデータ**”を生成し、ビデオの時系列上のどこからでも再生できるようにします。
サーバー上のファイル位置を変えた場合、シーク情報やメタデータも一緒に移動はしてくれません。これらは絶対パスを利用していますので、手動で削除し、再生成されるように仕向ける必要があります。




## HLSでのVODの対応

HLSは従来のVOD用途向けにデザインされていません。HLSはライブストリームから小粒度のファイルを生成して、iOSデバイス（iPhoneやiPad）に配信するようにデザインされています。iOSデバイスはオンラインソースからそれらのファイルをダウンロードし再生することができます。

EMSでHLSをつかってVODすることもできなくはありません。まず先にダミーでRTMPライブストリームを生成し、それから新規HLSストリームを生成するという方法がとれます。


サンプル手順:

```
Issue a pullStream command:
pullStream uri=rtmp://<SERVER_ADDRESS>/vod/video.mov keepAlive=1 localstreamname=DummyLive

Issue createHLSStream command:
createHLSStream localstreamnames=DummyLive bandwidths=128 targetfolder=../evo-webroot/ groupname=hls playlisttype=rolling playlistLength=10 chunkLength=20
```



## VOD再生でのストリームエイリアス有効化

エイリアス機能はVODストリームでも使用可能です。`hasStreamAliases`が有効化されていれば、ファイル名での再生はできなくなります。


VOD再生でエイリアス機能をつかって再生を行うには:

```
rtsp://<SERVER_ADDRESS>:5544/vod/<aliasname>
rtmp://<SERVER_ADDRESS>/vod/<aliasname>
```
