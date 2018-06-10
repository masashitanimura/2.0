---
title: VOD
keyword: vod
sidebar: userguide_sidebar
permalink: userguide_vod.html
folder: userguide
toc: false
---

VODページはEMSメディアフォルダ内のストリームにアクセスします。VODファイルの**再生** や **削除**が行えます。




1. サーバーのメディアフォルダをを選択してください

   ![](images/userguide/VOD_dir.JPG)

   ​

   **Note:** config.luaで指定したフォルダや [`addStorage`](api_addStorage.html)で指定したファルダ内のメディアがリスト表示されます

   ​

2. ファイルは自動的にリスト表示されます

   ![](images/userguide/VOD_load.JPG)

   ​

3. **Action**から下記のアクションを行えます

   - ![](images/userguide/VOD_play.JPG)   **再生** - メディアフォルダ内のVODファイルを再生します
   - ![](images/userguide/VOD_delete.JPG)   **削除** - メディアフォルダ内のVODファイルを削除します




## Playing VOD

UIをつかって、VODファイルをストリーム再生することができます。リストから選択し、Playボタンをクリックして再生できます


![](images/userguide/vod_playvod.JPG)

VODページで再生できるファイル:

- MP4
- TS
- FLV
- VOD  (.vod)  [generateLazyPull](api_generateLazyPullFile.html)で生成されたもの
- Playlist files (.lst) [generateServerPlaylist](api_generateServerPlaylist.html)で生成されたもの

------

## Notes:

- ブラウザでFlashを有効化してください
- 再生インスタンスごとに新規ウインドウが開きます
- JSplayer version 5.8.8が再生に使用されます　Firefoxは対応していませんので、代わりにChromeをご使用ください。
