---
title: config.lua
keywords: configuration
sidebar: userguide_sidebar
permalink: userguide_configlua.html
folder: userguide
toc: true
---

 EMSの主要な設定ファイルです。サーバーが使う起動パラメーターが記述されています。他のすべての設定ファイルのパスやファイル名も記述されており、必要ならこれらの設定ファイルを別名に変更することができます。config.luaファイルの記述はEMS実行ファイルへのコマンドラインパラメーターでもあります。EMSディストリビュー ションに付属する実行スクリプトはデフォルトで本ファイルを使用します。この実行スクリプトのパスやファイル名を変更することも可能です。

EMS設定ファイルであるconfig.luaは階層データ構造(keyとvalue)を持ち。Evostreamサーバー実行時のパラメータとして利用されます。書式は以下のようになります:

- **`<key>= <value>`**

  `value`には下記のような値が入ります:

  - 文字列(string) = 一連の英数字 (ダブルクオーテーションで囲む必要があります)

    ```
    例:	pushPullPersistenceFile="..\\config\\pushPullSetup.xml",
    ```

  - 数値(number) = 数字

    ```
    ​```
    例:	streamsExpireTimer=10,
    ​```
    ```

  - 配列(array) = 値のリスト (カンマで区切られ[]でグループ化、各値はダブルクオーテーションで囲む必要があります)/

    ```
    例:	aliases = {“flvplayback1”, “vod1”, “live”}
    ```

    ​


- **`<key名>= <object>`**

`object`は{}カッコで囲まれた割り当てリスト

  ```
  configurations =
  {
      daemon = "true",
      pathSeparator = "/",
      logAppenders = {...},
      applications = {...}
  }
  ```

  **Note:**

  ファイルを変更した後、サーバーが起動に失敗するようであれば、何らかの記入間違いをした可能性があります。変更をもとに戻すかまたは、コマンドラインパラメータで`--use-implicit-console-appender`オプション付きで実行し、起動時の問題についての詳細情報を確認してください。


  - Linuxパッケージ:

    ```
    cd /usr/bin/evostreamms –use-implicit-console-appender /etc/evostreamms/config.lua
    ```

    - Linuxアーカイブ:

      ```
      cd EMS_INSTALL_DIRECTORY
      ./evostreamms --use-implicit-console-appender ../config/config.lua
      ```

    - ウインドウズ:

      ```
      cd EMS_INSTALL_DIRECTORY
      evostreamms --use-implicit-console-appender config\config.lua
      ```

  **Where:**

  EMS_INSTALL_DIRECTORYは、EvoStream Media Server Archiveディレクトリ下の`bin`ディレクトリです


  1. “daemon”の値が読み込まれるとサーバーはフォークしてデーモンとなるかコンソールモードで起動しつづけます
  2. “logAppenders”の値が読み込まれると、log appendersが初期化され実行状態となります。log appenderの設定に基づいてログが表示されます。
  3. “applications”の値が読み込まれる段になると、アプリケーションが完全実行状態となりサーバーがオンラインとなります。





## daemon

Linuxのみ。 **true** の場合daemon modeで起動します。**false**の場合はコンソールモードで起動します（開発時に役立ちます）
**Type:** ブーリアン

**必須かどうか:** 必須

```
daemon = false,
```



## instancesCount

Linuxのみ。 負荷分散可動するEMSサーバーの仮想インスタンス数。この設定が無い場合は、自動的に0が設定され複数インスタンスは無効化されます。
設定値が負の値の-1の場合は、自動的にCPU数に解釈されます。


**Type:** 数値

**必須かどうか:** 必須

```
instancesCount=-1
```

たとえば４コアのサーバーを使用する場合:

```
instancesCount=0 : 1 origin + 0 edge
  2593 ?        00:00:00 evostreamms

instancesCount=1 : 1 origin + 0 edge
  2593 ?        00:00:00 evostreamms

instancesCount=2 : 1 origin + 1 edge
  2593 ?        00:00:00 evostreamms
  2607 ?        00:00:00 evostreamms

instancesCount=3 : 1 origin + 2 edges
  2593 ?        00:00:00 evostreamms
  2607 ?        00:00:00 evostreamms
  2608 ?        00:00:00 evostreamms

instancesCount=4 : 1 origin + 3 edges
  2593 ?        00:00:00 evostreamms
  2607 ?        00:00:00 evostreamms
  2608 ?        00:00:00 evostreamms
  2609 ?        00:00:00 evostreamms

instancesCount=-1 : 1 origin + 3 edges
  2593 ?        00:00:00 evostreamms
  2607 ?        00:00:00 evostreamms
  2608 ?        00:00:00 evostreamms
  2609 ?        00:00:00 evostreamms
```



## pathSeparator

サーバーによって使用されるセパレーターの指定
例: UNIXシステムの場合は / ウインドウズの場合は.です
Luaスクリプトでは\はエスケープシーケンスですので注意が必要です。

**Type:** 文字列

**必須かどうか:** 必須

```
pathSeparator="/",
```



## logAppenders

log appenderのリスト
ここで設定されているappenderはすべてlogger内にロードされます。すべてのログメッセージはこれらのlog appenderに振り向けられます。ログレベル設定によりappenderはメッセージを記録します。“Logging”は“media”にたいして"保存"していることを意味します。(下記の例ではコンソールappenderとファイルが設定されています)


**Type:** オブジェクト

**必須かどうか:** 必須

```
logAppenders=
	{
		{
			name="console appender",
			type="coloredConsole",
			level=6
		},
		{
			name="file appender",
			type="file",
			level=6,
			fileName="..\\logs\\evostream",
			newLineCharacters="\n",
			fileHistorySize=100,
			fileLength=1024*1024,
			singleLine=true,
			clearLogsOnStart=false
		},
	},
```

**Log Appenders Structure テーブル**

|        Key        |  Type   | 必須かどうか | 内容                              |
| :---------------: | :-----: | :-------: | ---------------------------------------- |
|       name        | 文字列  |    必須   | appender名 pretty printルーチン内で使用 |
|       type        | 文字列  |    必須   | appenderタイプ `console`や`coloredConsole`はコンソールに出力します`coloredConsole` はログレベルに応じたカラー付きメッセージです。`file` log appenderはすべてのメッセージを指定ファイルに書き出します |
|       level       | 数値 |    必須   | ログレベル (**Log levels:** 0 FATAL, 1 ERROR, 2 WARNING, 3 INFO, 4 DEBUG, 5 FINE, 6 FINEST, -1 ログ無効) |
|     fileName      | 文字列  |    必須   | appenderタイプがfileの場合にはそのファイルパス |
| newLineCharacters | 文字列  |    必須ではない    | file appenderでの改行コード |
|  fileHistorySize  | 数値 |    必須ではない    | ログの最大保持数 この数値を超えると最も古いファイルから削除されます |
|    fileLength     | 数値 |    必須ではない    | file appenderのバッファサイズ        |
|    singleLine     | ブーリアン |    必須ではない    | yesの場合は複数行のログメッセージは一行にマージされます |
| clearLogsOnStart  | ブーリアン |    必須ではない    | **true**の場合、EMSは保存先フォルダを検索し、現行の.logファイルを除くすべての*.log"ファイルを削除します。file appenderタイプのみ |

**Note:** デーモンモードがtrueに設定されている場合、すべてのコンソールappenderは無視されます



## applications

サーバー内のすべてのアプリケーションが記述されます。起動時に使用する各アプリケーション属性を保持します。各アプリケーションは実行時に必要となる独自の属性情報があります。


Below are the objects inside applications:



### rootDirectory

アプリケーションサブフォルダを保持するフォルダ。パスが“/” または “" で始まる場合(OSに依る)は、絶対パスとして扱われ、それ以外はランタイムディレクトリからの相対パスとして扱われます。


**Type:** 文字列

**必須かどうか:** 必須

ウインドウズ:

```
rootDirectory=".\\",
```

Linux:

```
rootDirectory="./",
```



### appDir

rootDirectoryとともに結合され、相対パスのベースディレクトリ


**Type:** 文字列

**必須かどうか:** 必須

ウインドウズ:

```
appDir=".\\",
```

Linux:

```
appDir="./",
```

**Note:** 相対パスを使用する場合のアプリケーションディレクトリの場所に注意してください。ファイルの保存場所はこの設定に左右されます。



### name

サーバー名。会社名や組織名その他で構いません

**Type:** 文字列

**必須かどうか:** 必須ではない

```
name="evostreamms",
```



### description

上記"name"の詳細情報

**Type:** 文字列

**必須かどうか:** 必須ではない

```
description="EVOSTREAM MEDIA SERVER",
```



### default

デフォルトアプリケーションを選択

**Type:** ブーリアン

**必須かどうか:** 必須

```
default=true,
```



### pushPullPersistenceFile

pushPull設定ファイルのパス

**Type:** 文字列

**必須かどうか:** 必須

```
pushPullPersistenceFile="..\\config\\pushPullSetup.xml",
```



### authPersistenceFile

認証用ファイルのパス

**Type:** 文字列

**必須かどうか:** 必須

```
authPersistenceFile="..\\config\\auth.xml",
```



### connectionsLimitPersistenceFile

接続数制限ファイルのパス

**Type:** 文字列

**必須かどうか:** 必須

```
connectionsLimitPersistenceFile="..\\config\\connlimits.xml",
```



### bandwidthLimitPersistenceFile

帯域制限ファイルのパス

**Type:** 文字列

**必須かどうか:** 必須

```
bandwidthLimitPersistenceFile="..\\config\\bandwidthlimits.xml",
```



### ingestPointsPersistenceFile

ingest pointファイルのパス

**Type:** 文字列

**必須かどうか:** 必須

```
ingestPointsPersistenceFile="..\\config\\ingestpoints.xml",
```



### streamsExpireTimer

タイムアウトするまで、EMSがオーディオ／ビデオデータを何秒待つか

**Type:** Number

**必須かどうか:** 必須

```
streamsExpireTimer=10,
```



### rtcpDetectionInterval

RTSPセッション時にRTCPストリームを何秒待つか

**Type:** Number

**必須かどうか:** 必須

```
rtcpDetectionInterval=15,
```



### hasStreamAliases

ストリーム名エイリアスの有効・無効

**Type:** ブーリアン

**必須かどうか:** 必須

```
hasStreamAliases=false,
```

 [addStreamAlias](addStreamAlias.html)を参照



### hasIngestPoints

ingest pointの設定

**Type:** ブーリアン

**必須かどうか:** 必須

```
hasIngestPoints=false
```

[createIngestPoint](createIngestPoint.html)を参照



### validateHandshake

RTMPハンドシェイク確立機能の無い旧いFlashプレーヤー設定

**Type:** ブーリアン

**必須かどうか:** 必須

```
validateHandshake=false,
```



### aliases

エイリアスが追加可能なストリームの拡張子

**Type:** Array

**必須かどうか:** 必須

```
aliases={"er", "live", "vod"},
```



### maxRtmpOutBuffer

RTMPバッファに使用する最大バイト数

**Type:** 文字列

**必須かどうか:** 必須

```
maxRtmpOutBuffer=512*1024,
```



### maxRtspOutBuffer

EMSがRTSPバッファに使用する最大バイト数。最終トランスポートがRTP over TCPのRTSPのみ


**Type:** 文字列

**必須かどうか:** 必須

```
maxRtspOutBuffer=512*1024,
```



### hlsVersion

使用するHLSのバージョン HLSファイルを使用する場合事前に確認が必要

**Type:** Number

**必須かどうか:** 必須

```
hlsVersion=6,
```

Supported versions:

- HLS version 3
- HLS version 4
- HLS version 5
- HLS version 6

HLSについてくわしくは [ココ](https://developer.apple.com/library/content/referencelibrary/GettingStarted/AboutHTTPLiveStreaming/about/about.html)を参照してください。



### useSourcePts

trueの場合、アウトバウンドストリームはソースストリームのPTSを使用。それ以外の場合はプッシュストリームは0スタートとなる

**Type:** ブーリアン

**必須かどうか:** 必須

```
useSourcePts=false,
```



### enableCheckBandwidth

trueの場合、bandwidth.xlmを読み込む


**Type:** ブーリアン

**必須かどうか:** 必須

```
enableCheckBandwidth=true,
```

 [bandwidths.xml](userguide_bandwidthlimits.html)を参照



### vodRedirectRtmpIp

EMSがソースVODファイルを取得する他のサーバーのIP

たとえばローカルサーバーがvideo1ファイルを検索する場合、検索が失敗すると`vodRedirectRtmpIp`パラメータを参照し、値がある場合はvideo1の`pullStream`リクエストを行い、そこで得られたストリームをもとにして当初のクライエントからのリクエストに応えます。


**Type:** 文字列

**必須かどうか:** 必須ではない

```
vodRedirectRtmpIp="",
```

**Note:** mediaFolderのみにアクセスします。VODファイルがmediaFolderにあることが必要です



### forceRtmpDatarate

特定の設定で必要な場合のハードコードのvideoおよびaudioデータレート

**Type:** ブーリアン

**必須かどうか:** 必須

```
forceRtmpDatarate=false,
```



### sendRtspRangeHeaders

axisカメラで必要な設定項目

**Type:** ブーリアン

**必須かどうか:** 必須

```
sendRtspRangeHeaders=false,
```



### serverNameStreamPrefix

ストリーム名の接頭語としてサーバー名を付加する

**Type:** 文字列

**必須かどうか:** 必須ではない

```
serverNameStreamPrefix="",
```



### runWebServer

EMS Web Serverの起動時有効化

**Type:** ブーリアン

**必須かどうか:** 必須

```
runWebServer=true,
```



### runWebUI

EMS Web UIの起動時の有効化Enables EMS Web UI on startup

**Type:** ブーリアン

**必須かどうか:** 必須

```
runWebUI=true,
```



### mediaStorage

メディアストレージ設定

**Type:** オブジェクト

**必須かどうか:** 必須

```
mediaStorage = {
				recordedStreamsStorage="../media",
				{
					description="Default media storage",
					mediaFolder="../media",
				},
			},
```

media folderは以下の用途があります:

- `pullStream`したVOD ファイルの保存先
- `generateLazyPull`コマンドで生成するファイルの保存先
- recodeコマンドで録画したストリームの保存先




**Media Structure テーブル**

|          Key           |  Type  | 必須かどうか | 内容                              |
| :--------------------: | :----: | :-------: | ---------------------------------------- |
| recordedStreamsStorage | 文字列 |   必須    | ストリームの録画で使用するmediaフォルダへのパス |
|      description       | 文字列 |   必須ではない   | メディアストレージの詳細情報     |
|      mediafolder       | 文字列 |   必須    | メディアストレージフォルダのパス    |



**その他のオプションパラメータ:**

|          Key          |  Type   | 必須かどうか | 内容                              |
| :-------------------: | :-----: | :-------: | ---------------------------------------- |
|      metaFolder       | 文字列  |   必須ではない   | シークおよびメタファイルのパス |
|      enableStats      | ブーリアン |   必須ではない   | EMSが統計情報、VODファイルのシークおよびメタデータファイルを作成する場所。EMSに書き込み権限が必要です  |
|   clientSideBuffer    | number  |   必須ではない   | trueの場合VODファイルについての統計情報がメディアファイルと同名.statsファイルに記録されmetaFolderに保存ます。アクセス回数や転送バイト数などが記述されます。 |
|     keyframeSeek      | ブーリアン |   必須ではない   | RTMPクライエントへのVOD再生時にEMSがバッファする秒数 |
|    seekGranularity    | number  |   必須ではない   | trueの場合シークはキーフレームでのみで行われます、falseの場合はシークはインターフレームパケットで行われ、この場合クライエントプレーヤー上でノイズとなることがあります |
| externalSeekGenerator | ブーリアン |   必須ではない   | mediaFolder内でのシークにかける秒数を厳守する |

[addStorage](addStorage.html)を参照



### acceptors

設定ファイル内の"evostream"の"application"セクション内の"acceptors"ブロックに記述されています。アプリケーションで使用するaccpetorプロトコルが定義されています。プロトコルによっては付随的なパラメータが必要となります。


**Type:** オブジェクト

**必須かどうか:** 必須

```
-- CLI acceptors
				{
					ip="0.0.0.0",
					port=1112,
					protocol="inboundJsonCli",
					useLengthPadding=true
				},
				{
					ip="0.0.0.0",
					port=7777,
					protocol="inboundHttpJsonCli"
				},
				{
					ip="0.0.0.0",
					port=9999,
					protocol="inboundHttpFmp4"
				},
				{
					ip="0.0.0.0",
					port=1222,
					protocol="inboundAsciiCli",
					useLengthPadding=true
				},
```

```
-- RTMP and clustering
				{
					ip="0.0.0.0",
					port=1935,
					protocol="inboundRtmp",
				},
				{
					ip="127.0.0.1",
					port=1936,
					protocol="inboundRtmp",
					clustering=true
				},
				{
					ip="127.0.0.1",
					port=1113,
					protocol="inboundBinVariant",
					clustering=true
				},
```

```
-- RTSP
				{
					ip="0.0.0.0",
					port=5544,
					protocol="inboundRtsp",
					--[[
					multicast=
					{
						ip="224.2.1.39",
						ttl=127,
					}
					]]--
				},
```

```
-- LiveFLV ingest
				{
					ip="0.0.0.0",
					port=6666,
					protocol="inboundLiveFlv",
					waitForMetadata=true,
				},
```

```
-- Inbound TCP TS
				{
					ip="0.0.0.0",
					port=9998,
					localStreamName="testTcp",
					protocol="inboundTcpTs",
				},
```

```
-- Inbound UDP TS
				{
					ip="0.0.0.0",
					port=9898,
					localStreamName="testUdp",
					protocol="inboundUdpTs",
				},
```

```
--RTMPS
				{
					ip="0.0.0.0",
					port=4443,
					protocol="inboundRtmp",
					sslKey="/path/to/some/key",
					sslCert="/path/to/some/cert",
				},
```

```
-- JSONMETA
				{
					ip="0.0.0.0",
					port=8100,
					--streamname="test",
					protocol="inboundJsonMeta",
				},
```

```
-- WebSockets JSON Metadata
				{
					ip="0.0.0.0",
					port=8210,
					protocol="wsJsonMeta",
					-- streamname="~0~0~0~"
				},
```

```
-- WebSockets JSON Metadata over SSL
				{
					ip="0.0.0.0",
					port=8433,
					protocol="wssJsonMeta",
					-- streamname="~0~0~0~"
					sslKey="/path/to/some/key",
					sslCert="/path/to/some/cert",
				},
```

```
-- WebSockets FMP4 Fetch
				{
					ip="0.0.0.0",
					port=8410,
					protocol="inboundWSFMP4"
				},
```

```
-- WebSockets over SSL FMP4 Fetch
				--[[
				{
					ip="0.0.0.0",
					port=8420,
					protocol="inboundWSSFMP4",
					sslKey="/path/to/some/key",
					sslCert="/path/to/some/cert",
				},
```



**Acceptor Structure テーブル:**

|   Key    |  Type  | 必須かどうか | 内容                              |
| :------: | :----: | :-------: | ---------------------------------------- |
|    ip    | 文字列 |   true    | サービスが提供されるIP 0.0.0.0の場合はすべてのインターフェースのすべてのIPを意味します |
|   port   | 文字列 |   true    | サービスが受け付けるポート番号 |
| protocol | 文字列 |   true    | ip:portの組み合わせであつかわれるプロトコルスタック |



**EMSによりサポートされるacceptor type:**

| Acceptor プロトコル  | よくある IP | よくある Port |    付加的パラメータ    | プロトコルスタック (Tags) |
| :----------------: | :--------: | :----------: | :-------------------------: | :-------------------: |
|   inboundJsonCli   | 127.0.0.1  |     1112     |      useLengthPadding       |     TCP+IJSONCLI      |
| inboundHttpJsonCli | 127.0.0.1  |     7777     |              -              | TCP+IHTT+H4C+IJSONCLI |
|  inboundAsciiCli   | 127.0.0.1  |     1222     |      useLengthPadding       |      TCP+IASCCLI      |
|    inboundRtmp     |  0.0.0.0   |     1935     |              -              |        TCP+IR         |
|    inboundRtmp     | 127.0.0.1  |     1936     |         clustering          |                       |
| inboundBinVariant  | 127.0.0.1  |     1113     |         clustering          |       TCP+BVAR        |
|    inboundRtsp     |  0.0.0.0   |     5544     |          multicast          |       TCP+RTSP        |
|   inboundLiveFlv   |  0.0.0.0   |     6666     |       waitForMetadata       |       TCP+ILFL        |
|    inboundTcpTs    |  0.0.0.0   |     9998     |       localStreamName       |        TCP+ITS        |
|    inboundUdpTs    |  0.0.0.0   |     9898     |       localStreamName       |        UDP+ITS        |
|    inboundRtmps    |  0.0.0.0   |     4443     |       sslKey, sslCert       |     TCP+ISSL+IRS      |
|  inboundJsonMeta   |  0.0.0.0   |     8100     |         streamname          |                       |
|     wsJsonMeta     |  0.0.0.0   |     8210     |         streamname          |                       |
|    wssJsonMeta     |  0.0.0.0   |     8433     | streamname, sslKey, sslCert |                       |
|   inboundWSFMP4    |  0.0.0.0   |     8410     |              -              |                       |
|   inboundWSSFMP4   |  0.0.0.0   |     8420     |       sslKey, sslCert       |                       |



**Protocol Group テーブル:**

|    Protocol Group    |   Tag    | Protocol Type          |
| :------------------: | :------: | ---------------------- |
|  Carrier Protocols   |   TCP    | TCP                    |
|         \|\|         |   UDP    | UDP                    |
|  Variant Protocols   |   BVAR   | Bin Variant            |
|         \|\|         |   XVAR   | XML Variant            |
|         \|\|         |   JVAR   | JSON Variant           |
|    RTMP Protocols    |    IR    | Inbound RTMP           |
|         \|\|         |   IRS    | Inbound RTMPS          |
|         \|\|         |    OR    | Outbound RTMP          |
|         \|\|         |    RS    | RTMP Dissector         |
| Encryption Protocols |    RE    | RTMPE                  |
|         \|\|         |   ISSL   | Inbound SSL            |
|         \|\|         |   OSSL   | Outbound SSL           |
|   MPEG-TS Protocol   |   ITS    | Inbound TS             |
|    HTTP Protocols    |   IHTT   | Inbound HTTP           |
|         \|\|         |  IHTT2   | Inbound HTTP2          |
|         \|\|         |   IH4R   | Inbound HTTP for RTMP  |
|         \|\|         |   OHTT   | Outbound HTTP          |
|         \|\|         |  OHTT2   | Outbound HTTP2         |
|         \|\|         |   OH4R   | Outbound HTTP for RTMP |
|    CLI Protocols     | IJSONCLI | Inbound JSON CLI       |
|         \|\|         |   H4C    | HTTP for CLI           |
|         \|\|         | IASCCLI  | Inbound ASCII CLI      |
|    RPC Protocols     |   IRPC   | Inbound RPC            |
|         \|\|         |   ORPC   | Outbound RPC           |
| Passthrough Protocol |    PT    | Passthrough            |



### deviceStreams

---

**Type:** オブジェクト

**必須かどうか:** 必須ではない

```
deviceStreams=
{
	{
		name="camera01",
		video=
		{
			type="v4l2",
			path="/dev/video0",
		},
		audio=
		{
			type="v4l2",
			path="/dev/video1",
		},
	},
},
```



**deviceStreams Structure テーブル**

|     Key      |  Type  | 必須かどうか | 内容 |
| :----------: | :----: | :-------: | ----------- |
|     name     | 文字列 |   true    |             |
| video - type | 文字列 |   true    |             |
| video - path | 文字列 |   true    |             |
| audio - type | 文字列 |   true    |             |
| audio - path | 文字列 |   true    |             |



### autoDASH/HLS/HDS/MSS

有効の場合、インジェストストリームから自動的にhttpストリームを生成します

**Type:** オブジェクト

**必須かどうか:** 必須ではない

```
autoDASH=
			{
				targetFolder="path/to/evo-webroot",
			},
autoHLS=
			{
				targetFolder="path/to/evo-webroot",
			},
autoHDS=
			{
				targetFolder="path/to/evo-webroot",
			},
autoMSS=
			{
				targetFolder="path/to/evo-webroot",
			},
```



**Note:** APIに付加的なパラメータをつけることができます。詳しくは [createDASHStream](api_createDASHStream.html),[createHLSStream](api_createHLSStream.html), [createHDSStream](api_createHDSStream.html), [createMSSStream](api_createMSSStream.html)をご参照ください。上記のauto使用時は下記のパラメータについては変更できません:

| パラメータ            |  Value  |
| -------------------- | :-----: |
| keepAlive            |  false  |
| cleanupDestination   |  true   |
| createMasterPlaylist |  false  |
| overwriteDestination |  true   |
| playlistType         | rolling |



### authentication

RTMPおよびRTSPプロトコルの認証設定。RTMPではこれに加え`auth.xml`ファイルが必要です。また`users.lua`ファイルにユーザ名・パスワードが記述されています。


**Type:** オブジェクト

**必須かどうか:** 必須ではない

```
authentication=
			{
				rtmp=
				{
					type="adobe",
					encoderAgents=
					{
						"FMLE/3.0 (compatible; FMSc/1.0)",
						"Wirecast/FM 1.0 (compatible; FMSc/1.0)",
						"EvoStream Media Server (www.evostream.com)"
					},
					usersFile="path/to/config/users.lua",
					--verifierUri="http://authserver/verifier.php",
					--token="secretstring",					
				},
				rtsp=
				{
					usersFile="path/to/config/users.lua",
					--authenticatePlay=false,
				}
				--ws=
				--{
				--	token="",
				--},
			},
```



**Authentication Structure テーブル:**

- **RTMP**

  |      Key      |  Type  | 必須かどうか | 内容                              |
  | :-----------: | :----: | :-------: | ---------------------------------------- |
  |     type      | string |   true    | "adobe"                                  |
  | encoderAgents | string |   true    | 使用するエンコーダエージェント           |
  |   usersFile   | string |   true    | users.lua設定ファイルのパス |
  |  verifierUri  | string |   false   | ベリファイヤファイルのパス |
  |     token     | string |   false   | トークンベースの認証で使用されるトークン。トークンはシークレット文字列のハッシュ値、リクエストされたストリーム名、Unix時間による計算値です。 |

  **RTMP URI Token フォーマット:** rtmp://hostname/streamName?e=ValidUntilUnixTime&h=Token

Token = MD5 (SecretString + "/" + StreamName + "?e=" + ValidUntilUnixTime)

  ```
  例: rtmp://127.0.0.1/live/bunny?e=1508895239&h=3C23875455CACF2D44C3608C146D7C87
  ```

  ​


- **RTSP**

  |       Key        |  Type   | 必須かどうか | 内容                              |
  | :--------------: | :-----: | :-------: | ---------------------------------------- |
  |    usersFile     | string  |   true    | users.luaファイルのパス |
  | authenticatePlay | ブーリアン |   false   | 有効の場合、プレーヤーはストリームリクエスト毎にパスワードを尋ねます |

  ​


- **WEBSOCKET**

  |  Key  |  Type  | 必須かどうか | 内容                              |
  | :---: | :----: | :-------: | ---------------------------------------- |
  | token | string |   true    | トークンベースの認証でトークンは使用されます。シークレット文字列のハッシュ値、リクエストされたストリーム名、Unix時間による計算値です。 |

 Token = MD5 (SecretString + "/" + StreamName + "?e=" + ValidUntilUnixTime)

  ​

  **トークン認証**
  The EMS accepts play requests that contains token authenticaion. Prior to serving the requested stream the EMS validates that the timestamp is for a time and date that is in the future. The EMS then recomputes the MD5 hash using the timestamp in the play request with the secret string and validates that the resultant hash value matches the value passed in on the play request. If any validation step fails, the EMS will not serve the requested stream. If all validation steps succeed, the EMS will serve the requested stream to the player.



**Notes:**

1. "config.lua"ファイル内の"authentication"ブロックの記述が無効か不完全な場合、認証機能は無効になります。RTMPプロトコルでは"auth.xml"ファイルが無いかまたは"false"に設定されていると認証機能は無効になります。RTSPプロトコルでは“rtsp”ブロックで**“authenticatePlay**”が無いか、"false"設定になっていると認証機能は無効になります。
2. Scripts are available for creating certificates and keys for EMS用の証明書とキーを生成するスクリプトが用意されています。くわしくは [GitHubファイル](https://github.com/EvoStream/evostream_addons/tree/master/certificates_and_keys)をご参照ください。
3. [UNIX time変換](http://www.onlineconversion.com/unix_time.htm) について
4. [MD5 hash生成](http://passwordsgenerator.net/md5-hash-generator/)




### eventLogger

event sink設定についてくわしくは [Events Overview](userguide_eventsoverview.html) をご参照ください

**Type:** オブジェクト

**必須かどうか:** 必須ではない



#### EMS Events Sinks

**A. File**

```
eventLogger=
	{
		--customData=123,
		sinks=
		{
			--[=[
			{
				type="file",
				--[[
				customData=
				{
					some="string",
					number=123.456,
					array={1, 2.345, "Hello world", true, nil}
				},
				]]--
				filename="C:\\EvoStream\\logs\\events.txt",
				format="text",
				--format="xml",
				--format="json",
				--format="w3c",
				--[[
				timestamp=true,
				appendTimestamp=true,
				appendInstance=true,
				fileChunkLength=43200, -- 12 hours (in seconds)
				fileChunkTime="18:00:00",
				]]--
				enabledEvents=
				{	-- common events enabled by default for eventLogger type "file":
					"inStreamCreated",
					"outStreamCreated",
					-- NOTE: add more events by copying items from the sorted list of VALID EVENTS below
				},
			},
```

**Notes:**

1. 本セクションはデフォルトで無効に設定されます

2. イベントリストにさらにイベントを付け加えることができます

3. イベントログファイルはEMSログ保存用パスに保存されます

4.  [イベントリスト](userguide_eventlist.html)を参照する

   ​

**File Sink Structure テーブル:**

|    Protocol     | Parameter | 必須かどうか | 内容                              |
| :-------------: | :-------: | :-------: | :--------------------------------------- |
|   customData    |  object   |    no     | sinkにより生成されたすべてのイベントに追記されるカスタムデータ。上位レベルで定義されたカスタムデータより優先されます。より複雑な階層構造を持つこともできます |
|      type       |  string   |    yes    | sinkタイプ “file”                 |
|    filename     |  string   |    yes    | ファイルのベースネーム                |
|     format      |  string   |    yes    | ファイルフォーマット **text**, **xml**, **json** **w3c**などが使用可能です |
|    timestamp    |  ブーリアン  |    no     | trueの場合ログファイルはファイル名にタイムスタンプが追記されます |
| appendTimestamp |  ブーリアン  |    no     | タイムスタンプ追記オプション。trueの場合 タイムスタンプ (YYYYMMDD_HHmmSS)がすべてのログファイルに追記されます。falseの場合は４桁の連番が追記されます。デフォルトはtrueです |
| appendInstance  |  ブーリアン  |    no     | ランダムな４桁のインスタンスIDが追記されます。デフォルトはfalseです |
| fileChunkLength |  number   |    no     | 新規ファイル作成する秒数    |
|  fileChunkTime  |  string   |    no     | ログファイル分割する時間指定 HH:MM:SSフォーマットで記述します。 *Note: fileChunkLength および fileChunkTime の両方がある場合ファイル分割は行われません |
|  enabledEvents  |  object   |    no     | ログ記録されるイベント、設定されていなければすべてのイベントがログ記録されます。 W3Cでは　non-stream-related イベントは無視されます |



**B. RPC - EvoWebservices**

```
{
		type="RPC",
		url="http://127.0.0.1:4000/evowebservices",
		serializerType="JSON",
		enabledEvents=
		{	-- common events enabled by default for eventLogger type "RPC":
			"inStreamCreated",
			"inStreamClosed",
			"outStreamCreated",
			"outStreamClosed",
			"timerTriggered",
			"hdsMasterPlaylistUpdated",
			"hdsChildPlaylistUpdated",
			"hdsChunkClosed",
			"hdsChunkDeleted",							
			"hlsMasterPlaylistUpdated",
			"hlsChunkClosed",
			"hlsChunkDeleted",									
			"dashPlaylistUpdated",
			"dashChunkClosed",
			"dashChunkDeleted",									
		},
},
```

**Notes:**

1. 本セクションはデフォルトで有効に設定されます
2. 使用するevowebserviceに合わせてURLを編集してください (Node.js or PHP)。evowebservices [userguide](evowebservices_overview.html)を参照してください
3. EMS webserviceによって使用されるイベントも記述されており、編集は不要です this configuration




**C. RPC - WebUI**

```
{
	type="RPC",
	url="http://127.0.0.1:4100/streams/update-list",
	serializerType="JSON",
	enabledEvents=
	{	-- common events enabled by default for eventLogger type "RPC":
		"inStreamCreated",
		"inStreamClosed",
		"outStreamCreated",
		"outStreamClosed",
		"processStarted",
		"processStopped",
		"recordChunkCreated",
		"recordChunkClosed",
		"webRtcServiceStarted",
		"webRtcServiceStopped",
	},
}
```

**Note:**

- EMS Web UIにより使用されるイベント 設定変更の必要はありません




### トランスコーダー

applicationセクションでEvoStream Transcoderの設定が記述されています。デフォルト設定のままで通常問題ありませんが、場合によっては変更が必要があります。


**Type:** オブジェクト

**必須かどうか:** 必須

```
transcoder = {
				scriptPath="..\\emsTranscoder.bat",
				srcUriPrefix="rtsp://localhost:5544/",
				dstUriPrefix="-f flv tcp://localhost:6666/"
			},
```

`srcUriPrefix`ではトランスコーダーがEMSからどのようにストリームを取得するかが記述されています。`dstUriPrefix`はトランスコーダーがEMSにストリームをプッシュするかについて記述されています。ポート番号はそれぞれのacceptorsに一致させる必要があります。デフォルト値はRTSPが`5544` LiveFLVが `6666`です。



**Transcoder Structure テーブル:**

|     Key      |  Type  | 必須かどうか | 内容                              |
| :----------: | :----: | :-------: | ---------------------------------------- |
|  scriptPath  | string |    yes    | トランスコーダーのヘルパースクリプトのパス。トランスコードAPI関数はバイナリを直接呼び出すのではなくスクリプトを経由します。これはカスタムトランスコーダーバイナリを使用するケースに対応しています。 |
| srcUriPrefix | string |    yes    | `transcode`API関数使用時にソースストリーム指定に`localStreamName`を使用できますが、その場合に付加される接頭語です。たとえば
 `srcUriPrefix="rtsp://localhost:5544"`と設定されており、ストリーム名が`"test1"`とトランスコードコマンドに与えられると、URIは `rtsp://localhost:5544/test1`が使用されます |
| dstUriPrefix | string |    yes    | srcUriPrefixの逆です。`localStreamName`がトランスコードコマンドに与えられると、設定された接頭語がストリーム名に付加されdestinationにむけて出力されます |



### mp4BinPath

mp4 writer実行ファイルのパス

**Type:** 文字列

**必須かどうか:** 必須

```
mp4BinPath="..\\evo-mp4writer.exe",
```



### webRTC

webRTCのセキュリティ設定

**Type:** オブジェクト

**必須かどうか:** 必須

```
webrtc = {
			sslKey="..\\config\\server.key",
			sslCert="..\\config\\server.cert",
		},
```



**webRTC Structure テーブル:**

|   Key   |  Type  | 必須かどうか | 内容                              |
| :-----: | :----: | :-------: | ---------------------------------------- |
| sslKey  | string |    yes    | sslキーのパス      |
| sslCert | string |    yes    | ssl証明書のパス |



### drm

DRM セクションはアクティブなDRMへの設定が記述されます。デフォルトではこのセクションはコメントされています(“–[[” と “]]–”で囲まれている)ので、DRMを有効化する前にこのセクションのコメントを外す必要があります。

**Type:** オブジェクト

**必須かどうか:**  HLSバージョン5使用時は必須

```
drm={
			type="verimatrix",
			requestTimer=1,
			reserveKeys=10,
			reserveIds=10,
			-- urlPrefix="http://server1.evostream1.com:12684/CAB/keyfile"
			urlPrefix="http://vcas3multicas1.verimatrix.com:12684/CAB/keyfile"
	},
```


**DRM Structure テーブル:**

|     Key      |  Type  |         必須かどうか         | 内容                              |
| :----------: | :----: | :-----------------------: | ---------------------------------------- |
|     type     | string |            yes            | 使用するDRMタイプ
“**verimatrix**” – はHLSでVerimatrix DRMを有効化 “**evo**” – HLSでAES暗号化を有効化 ”**none**” – DRM無効（セクションをコメントと同義） |

| requestTimer | number | yes, when type=verimatrix | キーリクエストタイマー秒数 EMSは起動後からタイマー秒数毎にVerimatrixキーサーバーにキーリクエストを行います Default=1, Min=1, Max=none (Minより低い数値が設定された場合はmin値が適用されます) |
| reserveKeys  | number | yes, when type=verimatrix | IDごとのキー数　Default=10, Min=5, Max=none (Minより低い数値が設定された場合はmin値が適用されます) |
|  reserveIds  | number | yes, when type=verimatrix | アクティブIDに加えキーバッファに充当するリザーブID数 Default=10, Min=5, Max=none. (Minより低い数値が設定された場合はmin値が適用されます) |
|  urlPrefix   | string | yes, when type=verimatrix | Verimatrix VCAS Key Serverの場所 |
