---
title: User Defined Variables
keywords: demo
sidebar: userguide_sidebar
permalink: userguide_userdefined.html
folder: userguide
toc: false
---

EMSは豊富なAPI関数を持っていますが、変数が足りない場合や個別ストリームにより多くの関連情報を付加させたいという場合があるかもしれません。これに対応するため、EMS APIでは*ユーザ定義変数*を実装しております。ユーザ定義変数はEMSが管理している情報（ストリームのプルやタイマー作成、トランスコードジョブの開始等）であればどのAPI関数からでも利用できます。

ユーザ定義関数を指定するにはアンダースコア(`_`)を編集の最初に使用します。コマンド（listStreamsやlistConfig等）についての情報が得られる場合はユーザ定義関数についてもリポートされます。

ユーザ定義変数のよくあるユースケースを下記に例示します:

```
setTimer value=120 _streamName=MyStreamsetTimer value=120 _streamID=5

```

指定時間経過後にストリームを停止するタイマー設定

```
pullstream uri=rtmp://192.168.1.5/live/myStream localstreamname=test1 _myID=5 _myName=secretSquirrel

```
ストリーム名とストリームidが設定されるコマンドのタイマーイベントが120秒後に実行される


1. ローカルストリームにカスタムidをつける

   ```
     pushstream uri=rtmp://192.168.1.5/live/myStream localstreamname=test1 _myID=5 _myName=secretSquirrel

   ```

カスタム値をプッシュストリームに設定する
