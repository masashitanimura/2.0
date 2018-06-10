---
title: Create HLS Stream
keywords: hls
sidebar: userguide_sidebar
permalink: userguide_createhls.html
folder: userguide
toc: true
---

H.264/AACおよびH.265/AACストリームからHTTP Live Stream (HLS)を生成します。HLSはiPhoneやiPad等iOS端末向けのライブフィードのストリーミングに使用されます。詳しくは`createHLSStream` [API](api_createHLSStream.html)をご参照ください。




## 手順

### シングルストリーム

**一般的なフォーマット:**

```
createHLSStream localstreamnames=<localstreamname> targetFolder=<target_folder_path> groupname=<groupname>

```

- **ウインドウズ:**

  ```
  createHLSStream localstreamnames=myStream targetfolder=C:\EvoStream\evo-webroot groupname=myHLSGroup
  ```


- **Linuxパッケージ:**

  ```
  createHLSStream localstreamnames=myStream targetfolder=/var/evo-webroot groupname=myHLSGroup
  ```

- **Linuxアーカイブ:**

  ```
  createHLSStream localstreamnames=myStream targetfolder=/path_to_evo-webroot groupname=myHLSGroup
  ```



生成されたファイルは自動的に`targetFolder`で指定されたパスに保存されます

```
evo-webroot:                           --> targetfolder
myHLSGroup                             --> groupname
- myStream                             --> localstreamname
-- segmentfile_1.ts                    --> segment_file
-- segmentfile_2.ts                    --> segment_file
-- segmentfile_X.ts                    --> segment_file
-- playlist.m3u8                       --> childplaylist_file
- playlist.m3u8                        --> masterplaylist_file

```



### 複数ストリーム

 **createHLSStream**コマンドをつかって複数の`localStreamNames`を生成する手順を次に示します:

**一般的なフォーマット:**

```
createHLSStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> targetFolder=<target_folder_path> groupname=<groupname>

```

- **ウインドウズ:**

  ```
  createHLSStream localstreamnames=myStream1,myStream2  targetfolder=C:\EvoStream\evo-webroot groupname=myHLSGroup
  ```

- **Linuxパッケージ:**

  ```
  createHLSStream localstreamnames=myStream1,myStream2  targetfolder=/var/evo-webroot groupname=myHLSGroup
  ```

- **Linuxアーカイブ:**

  ```
  createHLSStream localstreamnames=myStream1,myStream2  targetfolder=/path_to_evo-webroot groupname=myHLSGroup
  ```



生成されたファイルは`targetFolder`で指定したパスに自動的に保存されます

```
evo-webroot:                           --> targetfolder
myHLSGroup                             --> groupname
- myStream1                            --> localstreamname_1
-- segmentfile_1.ts                    --> segment_file
-- segmentfile_2.ts                    --> segment_file
-- segmentfile_X.ts                    --> segment_file
-- playlist.m3u8                       --> childplaylist_file_1
- myStream2                            --> localstreamname_2
-- segmentfile_1.ts                    --> segment_file
-- segmentfile_2.ts                    --> segment_file
-- segmentfile_X.ts                    --> segment_file
-- playlist.m3u8                       --> childplaylist_file_2
- playlist.m3u8                        --> masterplaylist_file
```



## JSON CLI レスポンス

**サンプル APIコール:**

```
createHLSStream localstreamnames=testpullstream targetfolder=/var/evo-webroot groupname=hls playlisttype=rolling
```

**JSON CLI レスポンス:**

```
Command entered successfully!
HLS stream created

    groupName: hls
    localStreamNames:
      -- testpullStream
    playlistName: playlist.m3u8
    playlistType: rolling
    targetFolder: /var/evo-webroot
```



## HLSプレイリストファイルの再生

Safariやその他のプレーヤーでストリームを再生するのは以下の手順です

**一般的なフォーマット:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<HLS_groupname>/<Subfolder>/<playlist_filename>
```

**サンプル URL:**

- **シングルストリーム**

  ```
  http://192.168.2.34:8888/myHLSGroup/playlist.m3u8
  ```


- **複数のストリーム**

  ```
  http://192.168.2.34:8888/myHLSGroup/myStream1/playlist.m3u8
  ```

  ```
  http://192.168.2.34:8888/myHLSGroup/myStream2/playlist.m3u8
  ```

  ```
  http://192.168.2.34:8888/myHLSGroup/myStream3/playlist.m3u8
  ```

プレーヤーはHLSプレイリストが読み込まれると自動的にストリームの再生を開始します



## DVR 再生

EMSはライブストリームの一時停止やリジューム再生などのDVR機能をサポートします。これはHLSプロトコルに内包された機能です。“`appending`”プレイリストタイプを使用するか、または`playlistLength`に大きな値を指定した“`rolling`”プレイリストを使用します。

サーバーサイドプレイリストで“local pulls”を利用してタイムシフトコンテンツやスケジュールコンテンツの生成もできます



## HLS リジューム

サーバーやストリームにリスタートがあった場合、HLSは既存のプレイリストにセグメントappendを行います。これは`createHLSStream`APIコマンドで`hlsResume`パラメータを指定することで可能となります。

このパラメータのデフォルト値は0(false)です

`createHLSStream`APIコマンドで`hlsResume`パラメータをつかう例です:

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling hlsResume=1
```



## オーディオのみのHLS

EMSはオーディオのみのHLS配信をサポートします

createHLSStream APIコマンドを`audioOnly`パラメータ付きとすることでビデオなしのストリームを生成します。このパラメータのデフォルト値は0(false)です

`audioOnly`パラメータ付きの`createHLSStream`コマンドの例:

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling audioOnly=1

```



## 暗号化

**Note:** 暗号化はHLSバージョン５以降でサポートされています



### VeriMatrix DRM

EMSはHLSストリームでVerimatrix DRMをサポートします。VeriMatrixサポートを有効化するにはconfig.luaファイル内で"drm"セクションの編集が必要です。 詳しくは[Configuration File]() の“drm” セクションをご参照ください

Verimatrixサポートが有効化されると、HLSストリームにVerimatrixプロテクションを条件付きで付加することができます。。drmTypeパラメータを`createHLSStream` コマンドで指定してください。

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling drmType=verimatrix
```



### AES暗号化

EMSはHLSストリームでAES暗号化をサポートします。AES暗号化を使用するには、`createHLSStream` コマンドで`drmType` と`aesKeyCount`の両方を指定する必要があります

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling drmType=ems aesKeyCount=5
```

- **drmType** では文字列型で暗号化の種類を指定します (“ems”は EvoStream AES encryption schemeを意味します).
- **aesKeyCount** は整数値型（デフォルト値は５）で暗号化されるHLSストリームのローテーションキー生成数を指定します。




## Automatic HLS

EMSは新規インバウンドストリームに対して自動的にHLSストリームを生成するよう設定することができます
詳細はconfig.luaファイルに記述され、`createHLSStream`APIコールでのパラメータ設定は不要です。

```
autoHLS=
{
    targetFolder= "/var/evo-webroot",
},
```

`config.lua`ファイルを編集については  [詳細](userguide_config.html#autoDASH/HLS/HDS/MSS)をご参照ください。

------

## 関連リンク:

- [createHLSStream API](api_createHLSStream.html)
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)
- [HLS Upload Service](evowebservices_HLSupload.html)
