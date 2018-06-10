---
title: Active Streams
keyword: liststreams
sidebar: userguide_sidebar
permalink: userguide_active.html
folder: userguide
toc: true
---

アクティブなストリームに関する情報を表示します。インバウンド、アウトバウンド、アダプティブHTTPストリームから選択してください。

![](images/userguide/activedropdown.jpg)



## インバウンドストリーム

アクティブなインバウンドストリームをリスト表示します

![](images/userguide/Active_inbound.JPG)

- ![](images/userguide/Config_info.JPG)   **情報表示** - ストリーム情報を表示します
- ![](images/userguide/VOD_play.JPG)   **再生** - インバウンドファイルを再生します
- ![](images/userguide/VOD_delete.JPG)   **削除** - ストリームを削除します




### インバウンドストリームの再生

アクティブなインバウンドストリームはWeb UI上で再生できます。再生ボタンをクリックすると再生を開始します


![](images/userguide/active_playhtml5.JPG)



**Notes:**

- HTML5プレーヤーにはevohtml5player-2.0.13.bundle.jsを使用します
- 再生には個別ウインドウが開きます





## アウトバウンドストリーム

アクティブなアウトバウンドストリームをリスト表示します

![](images/userguide/Active_outbound.JPG)

- ![](images/userguide/Config_info.JPG)   **情報表示** - ストリーム情報を表示します
- ![](images/userguide/VOD_delete.JPG)   **削除** - ストリームを削除します






## アダプティブHTTPストリーム

アクティブなHTTPストリームをリスト表示します

![](images/userguide/Active_http.jpg)



- ![](images/userguide/Config_info.JPG)   **情報表示** - ストリーム情報を表示します
- ![](images/userguide/VOD_play.JPG)   **再生** - HTTPファイルを再生します
- ![](images/userguide/VOD_delete.JPG)   **削除** - ストリームを削除します




**Note:**

- EMS内で更新があった場合、アクティブなページは自動的更新されます




## HTTPストリームの再生

Web UI上でHLSおよびDASHストリームを再生できます。再生ボタンをクリックすると再生を開始します



### HLSストリームの再生

![](images/userguide/active_playhls.JPG)



### DASHストリームの再生

![](images/userguide/active_playdash.JPG)

**Notes:**

- HLSプレーヤーはVideo.js HLS build version 2.0.1を使用します
- Video.js HLS build version 2.0.1はFirefoxブラウザではサポートされていません。代わりにChromeをお使いください
- DASHプレーヤーはDASH-IF v2.5.0-d389aedを使用します
- 再生ごとに個別のウインドウを開きます

------

## 関連リンク

- [listStreams]([](/api/listStreams.html))

  ​
