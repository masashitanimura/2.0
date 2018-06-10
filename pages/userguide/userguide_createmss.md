---
title: Create MSS Stream
keywords: mss
sidebar: userguide_sidebar
permalink: userguide_createmss.html
folder: userguide
toc: true
---

MSS (Microsoft Smooth Streaming)を生成します。再生デバイスで十分ネットの帯域およびビデオレンダリング機能が得られる場合、サンプルコンテンツのHDビデオ再生が可能で、さまざまな条件下でのユーザーエクスペリエンスをシュミレートすることができます。くわしくは [詳細](https://www.iis.net/media/experiencesmoothstreaming)



## 手順

### シングルストリーム

**一般的なフォーマット:**

```
createMSSStream localstreamnames=<localstreamname> bandwidths=<bandwidth> targetFolder=<target_folder_path> groupname=<groupname>
```

- **ウインドウズ:**

  ```
  createMSSStream localstreamnames=myStream bandwidths=51265536 targetfolder=C:\EvoStream\evo-webroot groupname=myMSSGroup
  ```


- **Linuxパッケージ:**

  ```
  createMSSStream localstreamnames=myStream bandwidths=51265536 targetfolder=/var/evo-webroot groupname=myMSSGroup
  ```

- **Linuxアーカイブ:**

  ```
  createMSSStream localstreamnames=myStream bandwidths=51265536 targetfolder=/path_to_evo-webroot groupname=myMSSGroup
  ```


生成されたファイルは`targetFolder`パスに自動的に保存されます


```
evo-webroot:                            --> targetfolder
myMSSGroup                              --> groupname
- myStream                              --> localstreamname
-- audio                                --> audio_folder
--- 51265536                            --> bitrate_folder
---- XXXXXXXXXX000.fmp4                 --> audio_segment_file
---- XXXXXXXXXXXXX.fmp4                 --> audio_segment_file
-- video                                --> video_folder
--- 51265536                            --> bitrate_folder
---- XXXXXXXXXX000.fmp4                 --> video_segment_file
---- XXXXXXXXXXXXX.fmp4                 --> video_segment_file
- manifest.ismc                         --> manifest_file
```



### Multiple Stream

 **createMSSStream**コマンドをつかって複数の`localStreamNames`を生成する手順を次に示します:


**一般的なフォーマット:**

```
createMSSStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> bandwidths=<bandwidth1,bandwidth2,bandwidthX> targetFolder=<target_folder_path> groupname=<groupname>
```

- **ウインドウズ:**

  ```
  createMSSStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=C:\EvoStream\evo-webroot groupname=myMSSGroup
  ```

- **Linuxパッケージ:**

  ```
  createMSSStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/var/evo-webroot groupname=myMSSGroup
  ```

- **Linuxアーカイブ:**

  ```
  createMSSStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/path_to_evo-webroot groupname=myMSSGroup
  ```


生成されたファイルは`targetFolder`パスに自動的に保存されます

```
evo-webroot:                           --> targetfolder
myMSSGroup                             --> groupname
- 10000000                             --> bitrate_folder_1
-- audio                               --> audio_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_audio_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_audio_file
-- video                               --> video_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_video_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_video_file
- 20000000                             --> bitrate_folder_2
-- audio                               --> audio_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_audio_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_audio_file
-- video                               --> video_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_video_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_video_file
- manifest.ismc                        --> manifest_file
```



## JSON CLI レスポンス

**サンプル API コール:**

```
createMSSStream localstreamnames=testpullstream,testpullstream bandwidths=10000000,20000000 targetfolder=../evo-webroot groupname=mss playlisttype=rolling
```

**JSON CLI レスポンス:**

```
Command entered successfully!
MSS stream created

    groupName: mss
    localStreamNames:
      -- testpullStream
    manifestName: manifest.ismc
    playlistType: rolling
    targetFolder: /var/evo-webroot
```



## Playing an MSS Manifest File

ストリームを再生するのは次の手順です:

**一般的なフォーマット:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<MSS_groupname>/<manifest_filename>
```

**サンプル URL:**

- **シングルストリーム**

  ```
  http://192.168.2.34:8888/myMSSGroup/manifest.ismc
  ```


- **複数のストリーム**

  ```
  http://192.168.2.34:8888/myMSSGroup/myStream1/manifest.ismc
  ```

  ```
  http://192.168.2.34:8888/myMSSGroup/myStream2/manifest.ismc
  ```

  ```
  http://192.168.2.34:8888/myMSSGroup/myStream3/manifest.ismc
  ```

The player will now automatically play the stream once the MSS manifest is read.



## Automatic MSS

EMSは新規インバウンドストリームに対して自動的にMSSストリームを生成するよう設定することができます
詳細はconfig.luaファイルに記述され、`createMSSStream`APIコールでのパラメータ設定は不要です。

```
autoMSS=
{
    targetFolder= "/var/evo-webroot",
},
```

`config.lua`ファイルを編集については  [詳細](userguide_config.html#autoDASH/HLS/HDS/MSS)をご参照ください。


------

- [createMSSStream API](api_createMSSStream.html)
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)
