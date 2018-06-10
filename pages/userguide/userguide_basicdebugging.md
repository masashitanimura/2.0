---
title: Basic Debugging
keywords: debug
sidebar: userguide_sidebar
permalink: userguide_basicdebugging.html
folder: userguide
toc: true
---

## EMSを起動できない

**Debug:**


1. **ライセンスファイルが適切に配置されているか**
2. **ライセンスの有効期限が切れていない**
3. **ポートが他のアプリケーションで使用されていないか、接続性に問題はないか**
4. **ネットワーク接続の確認**　オンラインライセンスの場合ネットワーク接続がないとライセンス検証ができません
5. **他のEMSインスタンスが起動済みでないか**
6. **EMSが正しくインストールされているか**
7. **日付と時刻が正確可** 日付と時刻は実時間に設定されている必要があります。日付と時刻の変更を検出するとEMSは実行されません
8. **テキストエディタの確認** config.luaファイルの編集などをおこなう際、使用するテキストエディタが余計な文字等を追加しないよう注意が必要です



------



## プル／プッシュしたストリームがストリーミングされない

**Debug:**

1. **事前確認事項**　ストリームソースがそもそもプレーヤーで再生可能かどうか確認


2. **`listConfig`を使用してストリームがプルされているかどうか確認**. ステータスはconnecting（接続中）ではなく **streaming** である必要があります

   ```
       pull:
         --
           configId: 1
           localStreamName: testpullStream
           status:
             current:
               description: Streaming
               uniqueStreamId: 1
           uri: rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4
   ```

3. **サーバーのアドレスが正しいか**

4. **localStreamNameが正しいか** EMSはlocalStreamNameを検索します。localStreamNameがみつからないとストリームはプッシュされません


------




## ストリームが録画されない

**Debug:**

1. **事前確認**　ストリームソースが実際にプレーヤーで再生可能かどうか確認
2. **pathToFileで指定したパスに書き込み権限はあるか**
3. **ネットワーク接続が安定しているか**


------



## Web UIの実行ができない

**Debug:**

1. ** config.luaの確認** `runWebUI`が`true`に設定されているか
2. **ポートが使用可能か** UIが使用するポートが使用可能か


------




## Web UIからのVODストリームができない

**Debug:**

1. **Flashが使用可能か** ブラウザでFlashが許可されているか

   ![](images/userguide/debug_flash.jpg)

   ​

2. **Google Chromeを使用する**  FirefoxではVideo. Jsプレーヤーはサポートされておらずストリームは再生できません。


------




## WebUIからHLSストリームができない

**Debug:**

1. **Google Chromeを使用する**  FirefoxではVideo. Jsプレーヤーはサポートされておらずストリームは再生できません。

------
