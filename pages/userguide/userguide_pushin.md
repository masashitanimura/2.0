---
title: Push-in a Stream
keywords: push-in
sidebar: userguide_sidebar
permalink: userguide_pushin.html
folder: userguide
toc: true
---

EMSは外部サーバーからプッシュされたストリームを受けることができます。RTMPリスナーはポート**1935**で受け付けています。RTSPリスナーは**5544**、LiveFLVリスナーは**6666**です。



## 手順

ソースストリームによってプッシュ方法は異なります。



## Push-In認証

セキュリティの観点からEMSは外部サーバーからプッシュされるストリームについて認証を必要とするよう設定ができます。認証設定は`config.lua`および`users.lua`に記述します。デフォルトでは認証設定は無効です。


下記の手順で認証機能を有効化します:

**Note:**


`../config`フォルダ以下のファイルを編集します

1. `auth.xml`のブーリアン値をtrueにします

   ```
    <BOOL name="">true</BOOL>

   ```

2. `config.lua`のauthenticationの部分のコメント(`--[[` .. `]]--`) を外し、必要なパラメータを設定します

   ```
    --[[ //remove
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
   					usersFile="/<path_to>/users.lua",
   					--verifierUri="http://authserver/verifier.php",
   					--token="secretstring",
   				},
   				rtsp=
   				{
   					usersFile="/<path_to>/users.lua",
   					--authenticatePlay=false,
   				},
   				--ws=
   				--{
   				--	token="",
   				--},
    },  
    ]]-- //remove
   ```

**認証パラメータ**

| プロトコル |  パラメータ名  | 内容                              |
| :------: | :--------------: | ---------------------------------------- |
|   RTMP   |       type       | RTMPタイプ                           |
|   \|\|   |  encoderAgents   | エンコーダーエージェント             |
|   \|\|   |    usersFile     | users fileへのパス               |
|   \|\|   |   verifierUri    | 外部URLベリファイヤ  200 OKという返り値は成功、その他は失敗です |
|   \|\|   |      token       | セキュリティトークン              |
|   RTSP   |    usersFile     | users fileへのパス               |
|   \|\|   | authenticatePlay | trueに設定すると、ストリーム再生リクエストの際、ユーザ名およびパスワードを求めるプロンプトが表示されます |



**users.luaでユーザー追加**

authenticatePlayがtrueに設定されている場合に認証ウインドウが表示されユーザー名およびパスワードが求められますが、
`users.lua`にユーザー名およびパスワードが設定されています。

```
users=
{
  USER_A="12345678",
}
realms=
{
  {
    name="EVOSTREAM stream router",
    method="Digest",
    users={
      "USER_A",
    },
  },
}

```

**Note:** 複数のユーザーを記述することができます

```
users=
{
  USER_A="12345678",
  USER_B="87654321",
}
realms=
{
  {
    name="EVOSTREAM stream router",
    method="Digest",
    users={
      "USER_A",
      "USER_B",
    },
  },
}
```

------

## 関連リンク:

- [pushStream API](pushStream.html)
- [Send Stream To Facebook](userguide_send.html#facebook-live)
- [Send Stream To Youtube](userguide_send.html#youtube-live)
