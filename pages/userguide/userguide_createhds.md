---
title: Create HDS Stream
keywords: hds
sidebar: userguide_sidebar
permalink: userguide_createhds.html
folder: userguide
toc: true
---


H.264/AACストリームからHDS (HTTP Dynamic Streaming)ストリームを生成します。HDSはHTTP経由でMP4メディアをストリームするのに使用されます。HDSはAppleのHLSに対してAdobeが開発した比較的新しい技術です。




## 手順

### シングルストリーム

**一般的なフォーマット:**

```
createHDSStream localstreamnames=<localstreamname> targetFolder=<target_folder_path> groupname=<groupname>
```

- **ウインドウズ:**

  ```
  createHDSStream localstreamnames=myStream targetfolder=C:\EvoStream\evo-webroot groupname=myHDSGroup
  ```


- **Linuxパッケージ:**

  ```
  createHDSStream localstreamnames=myStream targetfolder=/var/evo-webroot groupname=myHDSGroup
  ```

- **Linuxアーカイブ:**

  ```
  createHDSStream localstreamnames=myStream targetfolder=/path_to_evo-webroot groupname=myHDSGroup
  ```


生成されたファイルは`targetFolder`パスに自動的に保存されます


```
evo-webroot:                           --> targetfolder
myHDSGroup                             --> groupname
- myStream                             --> localstreamname
-- bootstrap                           --> boostrap_file
-- myStream1.f4m                       --> childplaylist_file
-- f4vSegXX-FragXX                     --> segment_chunk_file
- manifest.f4m                         --> masterplaylist_file
- manifest_v1.f4m                      --> masterplaylist_file
```



### 複数のストリーム

 **createHLSStream**コマンドをつかって複数の`localStreamNames`を生成する手順を次に示します:

**一般的なフォーマット:**

```
createHDSStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> targetFolder=<target_folder_path> groupname=<groupname>
```

- **ウインドウズ:**

  ```
  createHDSStream localstreamnames=myStream1,myStream2  targetfolder=C:\EvoStream\evo-webroot groupname=myHDSGroup
  ```

- **Linuxパッケージ:**

  ```
  createHDSStream localstreamnames=myStream1,myStream2  targetfolder=/var/evo-webroot groupname=myHDSGroup
  ```

- **Linuxアーカイブ:**

  ```
  createHDSStream localstreamnames=myStream1,myStream2  targetfolder=/path_to_evo-webroot groupname=myHDSGroup
  ```


生成されたファイルは`targetFolder`パスに自動的に保存されます


```
evo-webroot:                           --> targetfolder
myHDSGroup                             --> groupname
- myStream1                            --> localstreamname_1
-- bootstrap                           --> boostrap_file
-- myStream1.f4m                       --> childplaylist_file
-- f4vSegXX-FragXX                     --> segment_chunk_file
- myStream2                            --> localstreamname_2
-- bootstrap                           --> boostrap_file
-- myStream2.f4m                       --> childplaylist_file
-- f4vSegxx-Fragxx                     --> segment_chunk_file
- manifest.f4m                         --> masterplaylist_file
- manifest_v1.f4m                      --> masterplaylist_file
```



## JSON CLI レスポンス

**サンプル API コール:**

```
createHDSStream localstreamnames=testpullstream targetfolder=/var/evo-webroot groupname=hds playlisttype=rolling
```

**JSON CLI レスポンス:**

```
Command entered successfully!
HDS stream created

    groupName: hds
    localStreamNames:
      -- testpullStream
    manifestName:
    playlistType: rolling
    targetFolder: /var/evo-webroot
```



## HDS プレイリストファイルの再生

ストリームを再生するのは次の手順です:

**一般的なフォーマット:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<HDS_groupname>/<Subfolder>/<manifest_filename>
```

**サンプル URL:**

- **シングルストリーム**

  ```
  http://192.168.2.34:8888/myHDSGroup/manifest.f4m
  ```


- **複数のストリーム**

  ```
  http://192.168.2.34:8888/myHDSGroup/myStream1/manifest.f4m
  ```

  ```
  http://192.168.2.34:8888/myHDSGroup/myStream2/manifest.f4m
  ```

  ```
  http://192.168.2.34:8888/myHDSGroup/myStream3/manifest.f4m
  ```

プレーヤーはHDSプレイリストファイルを読み込むとストリームを自動的に再生します



## Automatic HDS

EMSは新規インバウンドストリームに対して自動的にHDSストリームを生成するよう設定することができます
詳細はconfig.luaファイルに記述され、`createHDSStream`APIコールでのパラメータ設定は不要です。


```
autoHDS=
{
    targetFolder= "/var/evo-webroot",
},
```

`config.lua`ファイルを編集については  [詳細](userguide_config.html#autoDASH/HLS/HDS/MSS)をご参照ください。

------

## 関連リンク:

- [createHDSStream API](api_createHDSStream.html)
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)
- [HDS Upload Service](evowebservices_HDSupload.html)
