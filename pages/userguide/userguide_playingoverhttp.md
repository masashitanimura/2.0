---
title: Play Over HTTP
keywords: http
sidebar: userguide_sidebar
permalink: userguide_playoverhttp.html
folder: userguide
toc: true
---

EMSはHTTP経由でのストリーム再生に対応しています

ブラウザで直接ストリーム再生を行い、ビデオタグにストリームを追加できます

**Note:**

対応はブラウザにもよります（対応はまちまちです）



## 手順

### Config.luaファイルの確認

```
{
	ip="0.0.0.0",
	port=9999,
	protocol="inboundHttpFmp4"
},
```

**Note:** 使用ポート番号の変更が可能です



### ブラウザでの再生

下記の書式でURLをブラウザで開きます

```
http://<IPofEMS:port>/<localStreamName>
```

```
http://127.0.0.1:9999/myStream
```

![](images/userguide/playoverhttp.jpg)



### ビデオタグの使用

下記の容量でURLをタグに埋め込みます：

```
<video src="http://<IPofEMS:port>/localStreamName"></video>
```
