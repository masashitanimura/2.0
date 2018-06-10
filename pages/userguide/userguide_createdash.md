---
title: Create DASH Stream
keywords: dash
sidebar: userguide_sidebar
permalink: userguide_createdash.html
folder: userguide
toc: true
---

H.264/AACストリームからDynamic Adaptive Streaming over HTTP (DASH)を生成します。DASHはMoving Picture Experts Group (MPEG)により開発されたHTTP アダプティブビットレートストリーミング規格で多数のベンダーに採用されています。



## 手順

### シングルストリーム

**一般的なフォーマット:**

```
createDASHStream localstreamnames=<localstreamname> bandwidths=<bandwidth> targetFolder=<target_folder_path> groupname=<groupname>
```

- **ウインドウズ:**

  ```
  createDASHStream localstreamnames=myStream bandwidths=51265536 targetfolder=C:\EvoStream\evo-webroot groupname=myDASHGroup
  ```


- **Linuxパッケージ:**

  ```
  createDASHStream localstreamnames=myStream bandwidths=51265536 targetfolder=/var/evo-webroot groupname=myDASHGroup
  ```

- **Linuxアーカイブ:**

  ```
  createDASHStream localstreamnames=myStream bandwidths=51265536 targetfolder=/path_to_evo-webroot groupname=myDASHGroup
  ```



生成されたファイルは`targetFolder`パスに自動的に保存されます

```
evo-webroot:                           --> targetfolder
myDASHroup                             --> groupname
- myStream                             --> localstreamname
-- audio                               --> audio_folder
--- 51265536                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> audio_segment_file
---- segment_XXXXX.m4s                 --> audio_segment_file
-- video                               --> video_folder
--- 51265536                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> video_segment_file
---- segment_XXXXX.m4s                 --> video_segment_file
- manifest.mpd                         --> masterplaylist_file
```



### 複数のストリーム


**createDASHStream**コマンドで複数の`localStreamNames`を生成するのは次の手順です

**一般的なフォーマット:**

```
createDASHStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> bandwidths=<bandwidth1,bandwidth2,bandwidthX> targetFolder=<target_folder_path> groupname=<groupname>
```

- **ウインドウズ:**

  ```
  createDASHStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=C:\EvoStream\evo-webroot groupname=myDASHGroup
  ```

- **Linuxパッケージ:**

  ```
  createDASHStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/var/evo-webroot groupname=myDASHGroup
  ```

- **Linuxアーカイブ:**

  ```
  createDASHStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/path_to_evo-webroot groupname=myDASHGroup
  ```



生成されたファイルは`targetFolder`パスに自動的に保存されます

```
evo-webroot:                           --> targetfolder
myDASHroup                             --> groupname
- myStream1                            --> localstreamname_1
-- audio                               --> audio_folder
--- 10000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> audio_segment_file
---- segment_XXXXX.m4s                 --> audio_segment_file
-- video                               --> video_folder
--- 10000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> video_segment_file
---- segment_XXXXX.m4s                 --> video_segment_file
- myStream2                            --> localstreamname_2
-- audio                               --> audio_folder
--- 20000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> audio_segment_file
---- segment_XXXXX.m4s                 --> audio_segment_file
-- video                               --> video_folder
--- 20000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> video_segment_file
---- segment_XXXXX.m4s                 --> video_segment_file
- manifest.mpd                         --> masterplaylist_file
```



## JSON CLI レスポンス

**サンプルAPIコール:**

```
createDASHStream localstreamnames=testpullstream targetfolder=/var/evo-webroot groupname=dash
```

**JSON CLI レスポンス:**

```
Command entered successfully!
DASH stream created

    groupName: dash
    localStreamNames:
      -- testpullStream
    manifestName: manifest.mpd
    playlistType: appending
    targetFolder: /var/evo-webroot
```



## DASH Manifestファイルの再生

ストリームを再生するのは次の手順です:

**一般的なフォーマット:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<DASH_groupname>/<manifest_filename>
```

**サンプルURL:**

- **シングルストリーム**

  ```
  http://192.168.2.34:8888/myDASHGroup/manifest.mpd
  ```


- **複数のストリーム**

  ```
  http://192.168.2.34:8888/myDASHGroup/myStream1/manifest.ismc
  ```

  ```
  http://192.168.2.34:8888/myDASHGroup/myStream2/manifest.ismc
  ```

  ```
  http://192.168.2.34:8888/myDASHGroup/myStream3/manifest.ismc
  ```

プレーヤーはDASH Manifestファイルを読み込むとストリームを自動的に再生します




## Automatic DASH

EMSは新規インバウンドストリームに対して自動的にDASHストリームを生成するよう設定することができます
詳細はconfig.luaファイルに記述され、`createDASHStream`APIコールでのパラメータ設定は不要です。

```
autoDASH=
{
    targetFolder= "/var/evo-webroot",
},
```

`config.lua`ファイルを編集については  [詳細](userguide_config.html#autoDASH/HLS/HDS/MSS)をご参照ください。


------

## 関連リンク:

- [createDASHStream API](api_createDASHStream.html)
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)
- [DASH Upload Service](evowebservices_DASHupload.html)
