---
title: Accessing the Run-Time API
keywords: API
sidebar: userguide_sidebar
permalink: userguide_telnet.html
folder: userguide
toc: true
---

EMS Web UIの他にtelnetやHTTPリクエストでEMSに接続することができます。下記はその手順です。



## 手動コマンドライン

**ウインドウズOSでの事前準備**

TelnetはWindows® OSでは明示的に有効化する必要がある場合があります。スタートメニューから コントロールパネル>プログラム>Windows機能の有効化または無 効化 をクリックし、Telnetクライエントを有効化してください。


![](images/userguide/enabletelnet.jpg)

またWindows OSではtelnetのlocal echoおよびnew line設定に若干の変更が必要です。
telnetが起動している場合は、ctrl+]でセッションから一旦exitし、下記コマンドを入力してください:


```
set localecho
set crlf
```

Windows telnetセッションに戻るには Enter または Return キーを押してください。





### ASCII CLI

ユーザが最初に触れるインターフェースはしばしばASCIIベースのインターフェースです。telnetアプリケーションやその他スクリプト言語を用いて簡単にアクセス可 能です。


config.luaでの設定:

```
{
	ip="0.0.0.0",
	port=1222,
	protocol="inboundAsciiCli",
	useLengthPadding=true
},
```

telnetインターフェースでAPIにアクセスするには、telnetアプリケーションがEMSが実行しているのと同じコンピューター上にある必要があります。telnetをopenするにはコマンドプロンプトで以下のようにします:


```
telnet localhost 1222
```

telnetセッションが開いたら、サーバーにコマンドを送りすぐに実行させることができます。 コマンドリクエストの例とその返り値は以下のようなものです。


**コマンドリクエスト:**

```
version
```

**レスポンス:**

```
Command entered successfully!
Version

    banner: EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491
with hash: 64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin/release/1.
7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)
    buildDate: 2016-06-17T09:33:23.000
    buildNumber: 4491
    codeName: PacMan|m|
    releaseNumber: 1.7.1
```



### ASCII JSON CLI

port 1112をつかってtelnetでAPIにアクセスすると、JSONでフォーマットされた返り値となります。CGIやBASHスクリプトで便利です。 ***JSONレスポンスにおける最初のキャラクタはJASON payloadのLENGTHです***



**Please note that the first character returned by the JSON response is the LENGTH of the JSON payload, allowing you to allocate properly sized structures at runtime.**

Configuration in config.lua:

```
{
	ip="0.0.0.0",
	port=1112,
	protocol="inboundJsonCli",
	useLengthPadding=true
},
```
 telnetセッション開始とリクエスト/返り値の例を以下に挙げます:


```
telnet localhost 1112

```

コマンドリクエストの例とその返り値は以下のようなものです。


**コマンドリクエスト:**

```
version
```

**レスポンス:**

```
{"data":{"banner":"EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491 with hash:64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin\/release\/1.7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)","branchName":"origin\/release\/1.7.0.1","buildDate":"2016-06-17T09:33:23.000","buildNumber":"4491","codeName":"PacMan|m|","hash":"64b305253110afc4acd5aeaf87f0a0b0f9b53526","releaseNumber":"1.7.1"},"description":"Version","status":"SUCCESS"}
```



## HTTP JSON CLI

HTTPインターフェース経由でAPIにアクセスするには、ブラウザでHTTPリクエストをサーバーにおくるだけです。デフォルトで使用するポートは**7777**です。ポート番号は設定ファイル（config.lua）で変更可能です。



Configuration in config.lua:

```
{
	ip="0.0.0.0",
	port=7777,
	protocol="inboundHttpJsonCli"
},
```

一般的なhttpフォーマットのリクエストは以下のようなものです:

```
http://[EMS_IP]:7777/[API]
```

コマンドリクエストの例とHTTPセッションからのレスポンスは以下のようなものです:


**リクエスト:**

```
http://localhost:7777/version

```

**レスポンス:**

```
{"data":{"banner":"EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491 with hash:64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin\/release\/1.7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)","branchName":"origin\/release\/1.7.0.1","buildDate":"2016-06-17T09:33:23.000","buildNumber":"4491","codeName":"PacMan|m|","hash":"64b305253110afc4acd5aeaf87f0a0b0f9b53526","releaseNumber":"1.7.1"},"description":"Version","status":"SUCCESS"}
```



### 複数のパラメータを使用する

HTTPではAPI全関数が使用可能ですが、パラメータを入れる場合はフォーマットをbase64にする必要があります。


```
http://[EMS_IP]:7777/[API]?params=([base64_encoded_parameters])
```



#### base54にパラメータを変換する

`pullstream`コマンドでの例:

```
pullStream uri=rtsp://localhost:5544/vod/mp4.bunny.mp4 localStreamName=bunny keepAlive=1 forceTcp=1
```

1. パラメータ付きでコマンドを記述し: `uri=rtsp://localhost:5544/vod/mp4.bunny.mp4 localStreamName=bunny keepAlive=1 forceTcp=1`

2. base64コンバータで変換します:

   Encode [here](https://www.base64encode.org/).

   **変換されたパラメータ:**

   ```
   dXJpPXJ0c3A6Ly9sb2NhbGhvc3Q6NTU0NC92b2QvbXA0LmJ1bm55Lm1wNCBsb2NhbFN0cmVhbU5hbWU9YnVubnkga2VlcEFsaXZlPTEgZm9yY2VUY3A9MQ==
   ```

3. 	これをHTTPフォーマットでリクエストする場合は以下のようになります

   ```
   http://localhost:7777/pullstream?params= dXJpPXJ0c3A6Ly9sb2NhbGhvc3Q6NTU0NC92b2QvbXA0LmJ1bm55Lm1wNCBsb2NhbFN0cmVhbU5hbWU9YnVubnkga2VlcEFsaXZlPTEgZm9yY2VUY3A9MQ==
   ```



- **Base64**

radix–64形式でバイナリーデータを ASCII文字列フォーマットで表現するバイナリーテキストエンコードスキームのひとつです。base64エンコードはオンラインにあるエンコーダを使用することもできます。

- **PHPおよびJavaScript**

PHPおよびJavaScript関数を使うこともできます。これらの関数はHTTPインターフェースコールをwrappingしたものでEMS Web UIディレクトリで見出すことができます。

- **APIのセキュリティ**

ASCII APIはデフォルトで保護されており、外部コンピューターからのアクセスはできないようになっており、config.lua設定ファイルを編集することでこれを変更することもできますが、サーバーセキュリティを維持する観点から変更なさらないことを推奨します。

HTTPベースのAPIもデフォルトで保護されており、外部からのアクセスはできませんが、HTTP APIを外部アクセス許可とすることで便利なこともあります。この場 合セキュリティを確保するには別途EWSのProxy Authenticationを有効化することができます。これによりAPIコール毎にユーザ認証が必要となるため、EMS APIへの アクセスは認証されたアクセスのみとすることができます。

イベント通知の設定と受信について

EMSではランタイムで発生したイベントを通知することができます。これらのイベントはHTTPコールでフォーマットされて、必要なアドレスやポートに送ることが できます。
デフォルトでイベント通知機能は有効となっており、EMSインストールによって提供されたローカルwebサービスに対してイベントを送る設定となっています。Web サービスはデフォルトでは無効状態になっていますので、イベントが通知されてきても何もアクションはとりません。webサービスの有効化その他については EvoStream Web Serviceをご参照ください。
