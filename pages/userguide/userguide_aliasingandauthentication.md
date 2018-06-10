---
title: Security and Authentication
sidebar: userguide_sidebar
permalink: userguide_aliasingandauthentication.html
folder: userguide
toc: true
---

## Stream Aliasing（ストリームのエイリアス）

Stream Aliasingはオンラインコンテンツを保護するメカニズムで、インバウンドストリームにそれぞれ_Aliases_を割り当てることができます。Stream Alieasingが有効化されると、インバウンドストリームに直接アクセスすることはできなくなります。クライエントは各ストリームに割り当てられたエイリアスを指定してストリームを取得します。エイリアス機能が有効の場合には**localStreamName**をつかってのストリームのリクエストや再生ができなくなることにご留意ください。またエイリアス機能は**シングルユース**で、エイリアスをつかってのストリームリクエストは一回きりです。使用後はそのエイリアスは削除されます。これによりタイトなオンラインコンテンツへのアクセスコントロールが可能です。

Stream Aliasingは広く一般にサーバーを公開する場合のストリームの保護機能です。指定のウェブサイトやプレーヤー向けのみに向けたエイリアスを生成できます。エイリアスをつかってクライエントからのアクセスがつながれば、ストリームはそれ以外からのアクセスから保護されます。Stream Aliasingはconfig.luaの_hasStreamAliases_を_true_にすることで有効化します。


エイリアスは次のAPIコマンドで管理できます

- [addStreamAlias](addStreamAlias.html)
- [removeStreamAlias](removeStreamAlias.html)
- [listStreamAliases](listStreamAliases.html)
- [flushStreamAliases](flushStreamAliases.html)


### エイリアスの有効期限

エイリアスは通常は一回使用するまでとなりますが、ExpirePeriodパラメータを使用して、指定の期間が過ぎるとシステムにより自動的に削除させることができます。ExpirePeriodは整数値で正の整数のほかに負の整数も使用できます。



正の整数: エイリアスは一回のみの使用ではなくなり、有効期限がくるまで何度も使用できます。

```
expirePeriod=10
```

上記の場合エイリアスは10秒間有効で、その間何度でもエイリアスをつかったアクセスが可能です。


負の整数値: エイリアスは一回のみの使用で、指定値の絶対数での秒数後に自動で削除されます。

```
expirePeriod=-10
```

上記の場合、エイリアスが１度も使われなければ、10秒後には自動で削除されます。


0の場合: ExpirePeriodパラメータへの設定値が０の場合、エイリアスの有効期限は無しとなります。ストリーム名の変更などの用途に使用することができます。


### よくあるエイリアス設定

例: 課金/登録ユーザーのみへのアクセス提供

Stream Aliassingは、様々なクライエント認証方式に対応しています。なんらか既存の認証方式でクライエントの認証が完了したら、あとはEMSで`addStreamAlias`コマンドをつかってクライエント向けのリンクを発行するだけです。

ユーザーがセキュリティアカウントにログインし、正面ドアのカメラへのリンクをクリックしたとしたら、ウェブサーバーはそれに対して以下のような処理を行います:

1. ユーザーの現在のセッションのベリファイ
2. EMSに以下のコマンドを発行:
3. `addStreamAlias localstreamname=privateDoorCam aliasName=publicDoorCam`
4. 下記のようなリンクを持つ再生用ページ返す（例ではflashを使用）:
 `rtmp://MyServer/live/publicDoorCam`

ユーザーアプリまたはブラウザのどちらであっても一度ストリームが読み込まれ再生されると、エイリアスは自動的に削除されます。したがって第三者が盗聴などなんらかの方法で再生用のリンクを得たとしても、またはユーザー本人が再生用リンクをコピーして保存しておき、後でもう一度再生しようとアクセスしてもうまくいかないことになります。


## グループ名エイリアス

Stream Aliasingは接続ベースのプロトコル(RTMPやRTSP)でのみ使用可能ですが、HLSやDASHその他HTTPベースのプロトコルではどうなるのでしょうか？その場合はグループ名エイリアスを使用します。

EMS Web Server (EWS) API を使用してグループ名エイリアスの追加・削除・確認・リスト表示ができます。グループ名エイリアスはソースストリームを保護・隠蔽するようデザインされています。グループ名エイリアスがひとたび生成されると、元のグループ名はストリーム再生用リクエストには使えなくなります。またグループ名エイリアスがリクエストされるとそのグループ名エイリアスは削除されます。

グループ名エイリアスを有効化するには、_webconfig.lua_webサーバー設定ファイルで_hasGroupNameAliases_オプションをtrueに設定します。HLS/HDS/MSS/DASHストリームはグループ名エイリアスを追加するまえにあらかじめ作成しておく必要があります。

グループ名エイリアスは次のAPIコマンドで管理ができます:

- [addGroupNameAlias](addGroupNameAlias.html)
- [removeGroupNameAlias](removeGroupNameAliases.html)
- [getGroupNameByAlias](getGroupNameByAlias.html)
- [listGroupNameAliases](listGroupNameAliases.html)
- [flushGroupNameAliases](flushStreamAliases.html)

グループ名エイリアスの一般的なユースケースを下記に記します。このユースケースはHDSやMSS、DASHストリームの場合にも応用できます（createHLSstreamの部分をcreateHDSstream, createMSSstream,  createDASHstreamにそれぞれ置き換えるだけです）


HTTTPストリームタイプごとの互換プレーヤーに関する詳細はInteroperabilityセクションをご参照ください。

1\. HTTPストリームのセットアップ

- HLSストリームの生成:

  `createhlsstream localstreamnames=mystream targetfolder=/var/evo-webroot groupname=mygroup playlisttype=rolling cleanupdestination=1`

- HTTPストリーミングセッションをリスト表示:

  `listHttpStreamingSessions`

- HTTPストリームにグループ名エイリアスを追加

  `addGroupNameAlias groupName=mygroup aliasName=myalias`

2\. HTTPストリームの再生

- 互換プレーヤーを起動し

- エイリアスURIを開く

  `http://localhost:8888/myalias`

上記の場合、実際には下記を再生していることになります
 `http://localhost:8888/mygroup/mystream/playlist.m3u8`

EWSはグループ名エイリアスからプレイリストへの正しいパスを解釈します。



## インバウンド認証

EvoStream Media Server はサーバーにストリームがプッシュされる際に認証を求めるように設定することができます。
認証により外部ソースがサーバーに過負荷をかけないように保護します。ストリームのプッシュはTCPベースのプロトコル(RTMPやRTSP)でのみ有効です。EMSが使用する認証設定は`config/usrs.lua`ファイルに記述されています。

インバウンド認証を有効・無効にするには:


1. `config/config.lua`ファイルの"Authentication"セクションをアンコメント・コメントする
2. `config/auth.xml`設定値をtrue (有効) または false (無効)

RTMPインバウンド認証設定でのポイントは"Encoder Agent"の確認です。これはストリームソースが自らを定義するのに使用されます。
Encoder Agentsはいくつかしか存在せず、Adobe Flash Media Encoderの機能を模倣するものがほとんどです。EMSにストリームをプッシュする場合Encoder Agent文字列には以下のように設定する必要があります。


1. Encoder Agent文字列を以下のいずれかに変更:
   - FMLE/3.0 (FMSc/1.0に互換)
   - Wirecast/FM 1.0 (FMSc/1.0に互換)
   - EvoStream Media Server ( [www.evostream.com](http://www.evostream.com/))
2. Encoder Agent文字列をconfig.luaファイルのencoderAgentsに追加



## アウトバウンド認証

ストリームをプッシュする際に認証が必要な場合は、pushコマンドのURIの中に**ユーザ名** and **パスワード**を指定してください。


サンプルURIフォーマットは下記のようになります:

```
rtmp://ユーザ名:パスワード@IPアドレス:ポート/ストリーム/行き先
```

実際のpushstream コマンドは下記のようになります:

```
pushstream uri=rtmp://myname:mypass@192.168.1.5/live localstreamname=TestStream1 targetstreamname=PushedStream
```



## クライエント認証

RTSPクライエントにクライエント認証を設定することができます。config.luaファイルのauthenticationのrtspノードのセクションに"AuthenticatePlay" パラメータを指定して有効化します。有効化されるとすべてのRTSPクライエントがconfig.luaで設定したユーザ名／パスワードを使用しなければならなくなります。


## Encoder/User Agents

```
emulateUserAgent=FMLE/3.0\ (compatible;\ FMSc/1.0)
```

RTMPストリームをプッシュする際、EMSで使用するEncoder Agentの変更が必要な場合があります。Encoder Agent はソースストリームのように振る舞うソフトウェアを指定する文字列です。RTMPエンドポイントによってはウェルノウンソースからのストリームしか受け付けないことがあり、この場合`pushuStream`コマンドに_emulateUserAgent_パラメータを付けて解決します。FMLEを使うのが最適です。


**Note:** 空白（スペース）はエスケープする必要があります

User-Agent文字列で短縮形をつかうことができます。大文字・小文字は区別しません

| emulateUserAgent          | 使用されるEncoder Agent                             |
| ------------------------- | ---------------------------------------- |
| emulateUserAgent=evo      | EvoStream Media Server ( [www.evostream.com](http://www.evostream.com/)) |
| emulateUserAgent=FMLE     | FMLE/3.0 (compatible; FMSc/1.0)"         |
| emulateUserAgent=wirecast | Wirecast/FM 1.0 (compatible; FMSc/1.0)"  |
| emulateUserAgent=flash    | MAC 11,3,300,265                         |

**Note:** emulateUserAgentはデフォルトで evoに設定されています
