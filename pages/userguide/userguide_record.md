---
title: Record a Stream
keywords: record
sidebar: userguide_sidebar
permalink: userguide_record.html
folder: userguide
toc: true
---

インバウンドストリームをRecordします。recordコマンドをつかってユーザーはストリームの録画ができます。サーバーに新規ストリームが入ってきてない場合、録画すべきストリームリストの確認を行います。

FLV、MPEG-TS、MP4ファイル等でストリームを録画することができます。

**Note:** ストリームの先頭のフレームを録画したい場合はストリーム追加よりも前にrecord`コマンドを実行しておく必要があります。



## 手順

### Recording MP4ファイル

`record`コマンドのデフォルトフォーマットです

**一般的なフォーマット:**

```
record localstreamname=<localstreamname> pathtofile=../path_to_media/filename type=<fileType>
```

- **ウインドウズ:**

  ```
  record localstreamname=myStream pathtofile=C:\EvoStream\media\myRecord type=mp4
  ```


- **Linuxパッケージ:**

  ```
  record localstreamname=myStream pathtofile=/var/evostreamms/myRecord type=mp4
  ```

- **Linuxアーカイブ:**

  ```
  record localstreamname=myStream pathtofile=/path_to_media/myRecord type=mp4
  ```

**相対パス**も使用可能です:

```
record localstreamname=myStream pathtofile=../media/myRecord type=mp4
```
生成されたファイルは`pathtofile`パスに自動的に保存されます

```
media:                           --> targetfolder
-testRecord.mp4.info             --> mp4 file on creation                     
-testRecord.mp4.mdat             --> mp4 file on creation               
-testRecord.mp4.track1           --> mp4 file on creation   
-testRecord.mp4.track2           --> mp4 file on creation   
```

ストリームソースが終了または接続断となった場合、MP4ファイルはひとつにコンパイルされます:
 詳しくは [MP4 File Creation](userguide_record.html#mp4-file-creation)をご参照ください。

```
media:                           --> targetfolder
-testRecord.mp4                  --> completed mp4 file
```

`chunkLength`パラメータが与えられている場合:

```
media:                           --> targetfolder
-testRecord_part0000.mp4 	    --> completed mp4 file chunk
-testRecord_part0001.mp4.info    --> mp4 file on creation                    
-testRecord_part0001.mp4.mdat    --> mp4 file on creation          
-testRecord_part0001.mp4.track1  --> mp4 file on creation   
-testRecord_part0001.mp4.track2  --> mp4 file on creation   
```



#### MP4 ファイルの作成

MP4ファイル作成時、EMSは３つ（ビデオまたはオーディオのみ）ないし４つ（ビデオおよびオーディオ）のファイルを作成します

- filename.info

- filename.mdat

- filename.track1

- filename.track2 (only if audio and video)

  これらのファイルはRecordコマンドで指定した保存先フォルダに保存されます

  録画終了時またはEMSが新規チャンク作成するためにファイルをクローズする際、これらのファイルは.mp4ファイルとしてひとつにまとめられます。ファイルの先頭に"atoms"ヘッダを備えた最適化されたMP4ファイルが作成されます。



  **evo-mp4writer**バイナリを使用してEMSは複数のファイルからMP4ファイルを作成します


  なんらかの理由でMP4ファイルの作成ができなかった場合、手動でevo-mp4writerバイナリを使用してMP4ファイルを作成することができます。一般的にこのような不具合は録画中にEMSまたはサーバーがシャットダウンした際に起きます。



  evo-mp4writerのコマンド書式は以下です:

  ```
  evo-mp4writer -path=/path/to/file.mp4
  ```

  `-path`パラメータはrecordの`pathtofile` パラメータと一致させる必要があります

  上記コマンドがうまくいかない場合に備えて、`--recovery`パラメータを最後に加えておくこともできます:


  ```
  evo-mp4writer -path=/path/to/file.mp4 --recovery
  ```

  **Note:**  `--recovery` オプションは1.7.0または1.7.1バージョンでは廃止される予定です。このオプションは以前はmdatを変更せずにftypやmoovアトムを上書きすることで手間を省くことができましたが、現状はmoovもmdatも内部コードベースで常に処理されるためevo-mp4writerを手動で動作させる場合も無効となりました。

  ​

### Recording TS File

**一般的なフォーマット:**

```
record localstreamname=<localstreamname> pathtofile=../path_to_media/filename type=<fileType>
```

- **ウインドウズ:**

  ```
  record localstreamname=myStream pathtofile=C:\EvoStream\media\myRecord type=ts
  ```

- **Linuxパッケージ:**

  ```
  record localstreamname=myStream pathtofile=/var/evostreamms/myRecord type=ts
  ```

- **Linuxアーカイブ:**

  ```
  record localstreamname=myStream pathtofile=/path_to_media/myRecord type=ts
  ```

**相対パス**も使用可能です:

```
record localstreamname=myStream pathtofile=../media/myRecord type=ts
```

生成されたファイルは`pathtofile`パスに自動的に保存されます

```
media:                           --> targetfolder
-testRecord.ts  		       --> ts file         
```

`chunkLength`パラメータが与えられている場合:

```
media:                           --> targetfolder
-testRecord_part0000.ts          --> ts file chunk                     
-testRecord_part0001.ts          --> ts file chunk          
-testRecord_part0002.ts          --> ts file chunk         
-testRecord_part0003.ts          --> ts file chunk       
...
```

TSファイルの長さは`chunkLength`パラメータによって決まります。ストリームソースが終了または接続断となった場合はTSファイルはそのまま残ります。



### Recording FLV File

**一般的なフォーマット:**

```
record localstreamname=<localstreamname> pathtofile=../path_to_media/filename type=<fileType>
```

- **ウインドウズ:**

  ```
  record localstreamname=myStream pathtofile=C:\EvoStream\media\myRecord type=flv
  ```

- **Linuxパッケージ:**

  ```
  record localstreamname=myStream pathtofile=/var/evostreamms/myRecord type=flv
  ```

- **Linuxアーカイブ:**

  ```
  record localstreamname=myStream pathtofile=/path_to_media/myRecord type=flv
  ```

**相対パス**も使用可能です:

```
record localstreamname=myStream pathtofile=../media/myRecord type=flv
```

生成されたファイルは`pathtofile`パスに自動的に保存されます

```
media:                           --> targetfolder
testRecord.flv                   --> flv file
```

`chunkLength`パラメータが与えられている場合:

```
media:                            --> targetfolder
-testRecord_part0000.flv          --> flv file chunk                     
-testRecord_part0001.flv          --> flv file chunk          
-testRecord_part0002.flv          --> flv file chunk         
-testRecord_part0003.flv          --> flv file chunk       
...
```

FLVファイルの長さは`chunkLength`パラメータによって決まります。ストリームソースが終了または接続断となった場合はFLVファイルはそのまま残ります。



## JSON CLI レスポンス

**API コール:**

```
record localStreamName=testpullstream pathtofile=../media/testRecord type=mp4 overwrite=1
```

**JSON レスポンス:**

```
Command entered successfully!
Recording Stream

    chunkLength: 0
    configId: 5
    localStreamName: testpullstream
    pathToFile: ../media/testRecord
    type: mp4
```



## 録画の停止

録画しているストリームもEMSでは他のストリームと同様に扱われます。ネットワークに向けられるかわりにファイルとして保存されるだけです。したがって録画の停止のコマンドもストリームのシャットダウンと同じです。ストリームのシャットダウンと同様に録画書き出し中のファイルはクローズされます。ストリームが録画されていなかった場合（指定したストリーム名のストリームがなかった）は、録画はキャンセルされます。


------

## 関連リンク

- [record API](api_record.html)
- [Stream Recorder Service](evowebservices_streamrecorder.html)
