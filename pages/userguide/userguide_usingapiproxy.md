---
title: Using API Proxy Authentication
keywords: apiproxy
sidebar: userguide_sidebar
permalink: userguide_usingapiproxy.html
folder: userguide
toc: true
---

EMS v2.0からapiProxyはデフォルトで有効化されています。設定は
 [webconfig.json](userguide_webconfig.html#apiproxy)で確認できます:

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

Proxy認証はHTTPベースのEMS APIをセキュアに行う方法です。すべてのAPIコマンドはまずEWSを通り**ユーザ名** と **パスワード**で認証をパスしたコマンドだけがEMSに渡されます。当然APIコマンドの返り値も適切にルーティングされます。




## Proxy認証をつかってAPIコマンドを送る手順

Proxy認証をつかったAPIコールの書式:

```
http://userName:password@EMS_IP:EWS_PORT/pseudoDomain/command?params=([base64 encoded parameters])
```

**Note:** EWSポートはwebconfig.jasonのapplication > rootDirectory > portで設定されています。EMSは8888を使います



**パラメータ無しのコマンド:**

```
http://username:password@localhost:8888/apiproxy/version
```

**コマンド結果:**

![](images/userguide/proxyone.jpg)





**パラメータ付きのコマンド:**

パラメータはbase64フォーマットにエンコードされている必要があります。オンラインツールなどを利用してパラメータのエンコードを行い、"param="の後に付加します。

```
http://username:password@localhost:8888/apiproxy/pullstream?params=dXJpPQlydG1wOi8vczJwY2h6eG10eW1uMmsuY2xvdWRmcm9udC5uZXQvY2Z4L3N0L21wNDpzaW50ZWwubXA0IGxvY2Fsc3RyZWFtbmFtZT1teVN0cmVhbQ==
```



**コマンド結果:**

![](images/userguide/proxytwo.jpg)



**Note:**

- ブラウザはJSON Parser extensionを持っています
- ユーザ名・パスワードがURLにない場合は、ブラウザは入力を促します
