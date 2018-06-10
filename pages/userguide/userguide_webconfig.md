---
title: webconfig.json
keywords: webconfig
sidebar: userguide_sidebar
permalink: userguide_webconfig.html
folder: userguide
toc: true
---

EvoStream Web Server (EWS)の主要設定ファイルです。Web rootフォルダやキーおよび証明書、ホワイト／ブラックリスト、ログなどの重要なファイル位置を定義しています。
またHTTP portやグルーム名エイリアス、SSLモード、接続数/メモリ制限、mimeタイプなどその他の設定も含まれています。


**Contents:**

- configuration – EWSサーバーが必要とするすべての設定が含まれています

```
configuration =
  {
      logAppenders
      {
          -- content removed for clarity
      },
      applications =
      {
          -- content removed for clarity
      }
}
```

**webServer Configuration Structure Table:**

|     Key      |  Type  | 必須か | 内容                              |
| :----------: | :----: | :-------: | ---------------------------------------- |
|   loggers    | object |    必須    | log appenderが記述されています。各ログメッセージは列挙された適切なappenderに送られます。 |
| applications | object |    必須    | 読み込まれるアプリケーションが記述されています。その他いくつかの設定も含まれています。 |

webサーバー起動の際、次の一連の処理が行われます:

- `loggers`の設定値が読み込まれます。log appenderが初期化・実行されます。

- `applications`設定値が読み込まれます。この後すべてのアプリケーションが完全に機能する状態になりサーバーがオンラインになり処理を受けられるようになります。

  ​

## loggers

web server ログおよびログファイルの設定

```
"loggers":
	{
		"console":
		{
			"colorize": true,
			"json": false,
			"level": "silly"
		},
		"file":
		{
			"filename": "evo-webserver",
			"extension": "log",
			"dirname": "C:\\EvoStream_2.1\\logs",
			"json": false,
			"maxsize": 1048576,
			"level": "silly"
		}
},,
```
このセクションにlog appenderがリスト表記されています。このリストが初期化の際にloggerに読み込まれます。

ログは **コンソール** and **ファイル**の２種類があります

 **console** と設定すると、EMSコンソールログ用設定です。**file**はログ・ファイル用の設定です。


**webServer loggers Structure Table:**

|    Key    |  Type   | 必須かどうか | 内容                              |
| :-------: | :-----: | :-------: | ---------------------------------------- |
| colorize  | boolean |    必須    | **true** の場合、ログがカラー表示されます。ログタイプにより色は異なります。config.luaのcoloredConsoleに類似しています |
|   json    | boolean |    必須    | **true** の場合、ログはjsonフォーマットで表示・保存されます |
|   level   | string  |    必須    | ログレベル設定。設定ログレベルまたはそれ以下のレベルメッセージが記録されます。(**Log levels:** SILLY, DEBUG, VERBOSE, INFO, WARN, ERROR) |
| filename  | string  |    必須    | ファイル名のプレフィックス (fileName.xxxx.timestamp.log) |
| extension | string  |    必須    | ログ・ファイルの拡張子(fileName.xxxx.timestamp.extension) |
|  dirname  | string  |   必須ではない     | ログファイルの絶対パス |
|  maxsize  | number  |   必須ではない     | ログファイル最大サイズ(キロバイト) |



## application

このセクションにはサーバー内のアプリケーションがリストされます。サーバー起動時に読み込まれるアプリケーション属性が記述されています。各アプリケーションはその機能を実行するために必要な特定の属性情報がある場合があります。




### name

web サーバーアプリケーション名

```
"name": "webserver",
```

**Type:** 文字列

**必須かどうか:** 必須



### description

webサーバーアプリケーションの詳細情報

```
"description": "Built-In Web Server",
```

**Type:** 文字列

**必須かどうか:** 必須ではない



### port

webサーバーのlisten port

```
"port": 8888,
```

**Type:** 数値

**必須かどうか:** 必須



### emsPort

webサーバーがemsと通信するポート

```
"emsPort": 1113,
```

**Note:** config.luaファイルの **inboundBinVariant** acceptorと一致している必要があります

**Type:** 数値

**必須かどうか:** 必須



### webservicesPort

web サービスがemsと通信するポート

```
"webservicesPort": 4000,
```

**Type:** 数値

**必須かどうか:** 必須



### webuiPort

webUIがemsと通信するポート

```
"webuiPort": 4100,
```

**Type:** 数値

**必須かどうか:** 必須



### bindToIP

ホストに複数のNICがある場合に使用するIP


```
"bindToIP": "",
```

**Type:** 文字列

**必須かどうか:** 必須ではない



### sslMode

webサーバー使用時のssl設定

```
"sslMode": "disabled",
```

**Type:** 文字列

**必須かどうか:** 必須ではない

**使用可能な設定値:**

- disabled - HTTPをつかう

- enabled - HTTPSの使用を強制する

- automatic - HTTPでチェックし、HTTPSにフォールバック




### sslKeyFile

SSLキーファイルパス

```
"sslKeyFile": "../config/server.key",
```

**Type:** 文字列

**必須かどうか:** 必須ではない



### sslCertFile

SSL証明書ファイルパス

```
"sslCertFile": "../config/server.cert",
```

**Type:** 文字列

**必須かどうか:** 必須ではない



### enableIPFilter

trueの場合、ブラック/ホワイトリストが読み込まれます

```
"enableIPFilter": false,
```

**Type:** ブーリアン

**必須かどうか:** 必須ではない



### whitelistFile

ホワイトリストのファイルパス

```
"whitelistFile": "../config/whitelist.txt",
```

**Type:** 文字列

**必須かどうか:** 必須ではない



### blacklistFile

ブラックリストのファイルパス

```
"blacklistFile": "../config/blacklist.txt",
```

**Type:** 文字列

**必須かどうか:** 必須ではない



### hasGroupNameAliases

グループ名エイリアスの有効・無効を設定します。HTTPストリーミング(HLS, HDS, MSS、DASH, メディアファイル)をダイレクトアクセスから保護します。

```
"hasGroupNameAliases": false,
```

**Type:** ブーリアン

**必須かどうか:** 必須ではない



### webRootFolder

webrootフォルダのパス

```
"webRootFolder": "..\\evo-webroot",
```


**Type:** 文字列

**必須かどうか:** 必須



### mediaFileDownloadTimeout

メディアファイルダウンロードセッションのタイムアウト値

```
"mediaFileDownloadTimeout": 30,
```

**Type:** 数値

**必須かどうか:** 必須



### supportedMimeTypes

このセクションではmime typeに関連するファイル拡張設定が記述されています

```
"supportedMimeTypes":
	[
		{
			"extensions": "mp4,mp4v,mpg4",
			"mimeType": "video/mp4",
			"streamType":"",
			"isManifest":false
		},
		{
			"extensions": "flv",
			"mimeType": "video/x-flv",
			"streamType":"",
			"isManifest": false
		},
		{
			"extensions": "m3u,m3u8",
			"mimeType": "audio/x-mpegurl",
			"streamType": "hls",
			"isManifest": true
		},
		{
			"extensions": "ts",
			"mimeType": "video/mp2t",
			"streamType": "hls",
			"isManifest": false
		},
		{
			"extensions": "aac",
			"mimeType": "audio/aac",
			"streamType": "hls",
			"isManifest": false
		},
		{
			"extensions": "f4m",
			"mimeType": "application/f4m+xml",
			"streamType": "hds",
			"isManifest": true
		},
		{
			"extensions": "ismc,isma,ismv",
			"mimeType": "application/octet-stream",
			"streamType": "mss",
			"isManifest": true
		},
		{
			"extensions": "fmp4",
			"mimeType": "video/mp4",
			"streamType": "mss",
			"isManifest": false
		},
		{
			"extensions": "mpd",
			"mimeType": "application/dash+xml",
			"streamType": "dash",
			"isManifest": true
		},
		{
			"extensions": "m4s",
			"mimeType": "video/mp4",
			"streamType": "dash",
			"isManifest": false
		},
		{
			"//": "needed for supporting adobe player's crossdomain.xml",
			"extensions": "xml",
			"mimeType": "application/xml",
			"streamType": "",
			"isManifest": false
		}
	],
```

**webServer supportedMime Types Structure Table:**

|    Key     |  Type   | 必須かどうか | 内容                              |
| :--------: | :-----: | :-------: | ---------------------------------------- |
| extensions | string  |    必須    | ファイル拡張子         |
|  mimeType  | string  |    必須    | ファイル拡張子に関連付けるmimeタイプ |
| streamType | string  |   必須ではない     | HTTPストリームタイプ                  |
| isManifest | boolean |   必須ではない     | HTTPストリーミングで使用するマニフェストファイルがあるか |



### includeResponseHeaders

このセクションでは付加的なレスポンスヘッダ情報が記述されています

```
"includeResponseHeaders":
	[
		{
			"header": "Access-Control-Allow-Origin",
			"content": "*",
			"override": true
		},
		{
			"header": "User-Agent",
			"content": "Evostream",
			"override": false
		}
	],
```

**webServer includeResponseHeaders Structure Table:**

|   Key    |  Type   | 必須かどうか | 内容                              |
| :------: | :-----: | :-------: | ---------------------------------------- |
|  header  | string  |    yes    | レスポンスヘッダ                     |
| content  | string  |    yes    | レスポンスヘッダに特定の値 |
| override | boolean |    No     | 既存ヘッダある場合にオーバーライドするか |



### apiProxy

Proxy認証をつかってHTTPベースのEMS APIを保護します。すｂてのAPIコマンドはEWSをいったん通り、ユーザ名/パスワード認証が行われ、EMSにコマンドを渡します。また返り値は適切に呼び出し元に戻されます。


Proxy認証を有効化するには*webconfig.lua* 設定ファイル内の“apiProxy”セクションをアンコメントしてください。


```
"apiProxy":
	{
		"enable" : true,
		"authentication": "basic", 			
		"pseudoDomain": "apiproxy",
		"address": "127.0.0.1",
		"port": 7777,
		"userName": "username",
		"password": "password"
	}
```
**apiProxy Structure Table:**

|      Key       |  Type   | 必須かどうか | 内容                              |
| :------------: | :-----: | :-------: | ---------------------------------------- |
|     enable     | boolean |    yes    | trueの場合、apiProxy設定が読み込まれます |
| authentication | object  |    yes    | 認証タイプ設定 ユーザー／パスワードを使う“**basic**”HTTP認証または認証をしない“**none**”の２つの設定値しかとれません。 |
|  pseudoDomain  | object  |    yes    | ドメイン名またはフォルダ                |
|    address     | number  |    yes    | inboundHTTPJsonCLIをしようするIPアドレス |
|      port      | number  |    yes    | Port, config.luaで設定した [inboundHttpJsonCli](http://docs.evostream.com/2.0/userguide_configlua.html#acceptors)用のacceptorポート |
|    userName    | string  |    No     | ベーシック認証ユーザ名            |
|    password    | string  |    No     | パスワード                |

 [Using API Proxy Authentication](userguide_usingapiproxy.html)を参照
