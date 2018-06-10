---
title: Configuring and Receiving Event Notifications
keywords: events
sidebar: userguide_sidebar
permalink: userguide_confevents.html
folder: userguide
toc: false
---

EMSはランタイム時に起きたイベントをもとにした通知を生成します。イベントはHTTPコール書式で指定したアドレス／ポートに配信することが可能です。

Event Notificationはデフォルトで有効化されており、EMSインストールの際に含まれているWebサービス宛てに送信するよう設定されています。
一方Webサービスはデフォルトでは**有効化されておらず**、イベントが送られてきてもなにもアクションを起こしません。webサービスの有効化と使用方法についてはEvoStream Web Servicesの資料を参照してください


イベント通知の宛先を追加的に指定することが可能で、`config.lua`ファイルを編集することで設定、有効化・無効化等が行えます。

イベント通知を有効化するにはconfig.luaファイルの*eventLogger*セクションのコメントを外す必要があります。LUAスクリプトでのコメントは一行の場合は`--` で複数ブロックに渡る場合は`--[[`から`]]--` までで指定できます。デフォルトではeventLoggerセクションはブロックスタイルでコメントされておりますので、`--[[` と `]]--`の２つを削除することでアンコメントできます。詳しくはConfiguration Filesセクションをご参照ください。
