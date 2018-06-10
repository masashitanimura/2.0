---
title: File Descriptions
sidebar: userguide_sidebar
permalink: userguide_filedescriptions.html
folder: userguide
toc: true
---

## コマンドファイル

| ファイル名             | 内容                              |
| --------------------- | ---------------------------------------- |
| emsTranscoder.bat     | EMSトランスコーダーバイナリ            |
| evo-avconv(.exe)      | The EvoStreamトランスコーダーバイナリ。 `transcode` APIコマンドにより呼び出されます |
| evo-mp4writer(.exe)   | さまざまなMP4収録ファイルをファイナライズするバイナリアプリケーション |
| evo-node(.exe)        | EvoStream Web Server (EWS) バイナリ。 HTTP経由でのすべてのファイルサービスを扱います |
| evostreamms(.exe)     | EvoStream バイナリ本体             |
| run_console_ems.bat   | EMSをコンソールアプリケーションとして実行するバッチファイル／スクリプト。 コマンドに対するフィードバックやエラーなどがすぐに確認できるので初心者に便利です |
| run_console_webui.bat | EMS Web UIアプリケーションを実行するバッチファイル／スクリプト。 UIとコンソールを分けて使いたい際に便利です。コマンドに対するフィードバックやエラーなどがすぐに確認できるので初心者に便利です。 |
| run_stop_webui.bat    | EMS Web UIアプリケーションを**停止する**バッチファイル／スクリプト |
| run_daemon_ems.sh     | **Linux/Unix** 環境においてEMSをバックグラウンドで実行するシェルスクリプト。スクリプト実行のためには"evostream"というユーザーが必要です。スクリプトを編集して別のユーザー権限で実行させることも可能です。daemonの実行状況を確認するには `ps –ef`を実行してください |
| run_console_ems.bat   | Batch file/script on **Windows**環境でEMSをコンソールアプリケーションとして実行するためのバッチファイル／スクリプト。コマンドに対するフィードバックやエラーなどがすぐに確認できるので初心者に便利です。  |



## Windows サービス

| ファイル名      | 内容                              |
| ------------- | ---------------------------------------- |
| create.bat    | EMSウインドウズサービスを生成するスクリプト。本スクリプトはEMSをバックグラウンドプロセスとして実行します。レジストリの変更を行うため管理者権限で実行する必要があります。*実行が必要なのは１回のみです* |
| remove.bat    | EMSウインドウズサービスを削除するスクリプト。レジストリからも適宜削除されます。管理者権限で実行する必要があります。|
| start.bat     | EMSウインドウズサービスを開始するスクリプト。上記のcreate.batが先に実行されている必要があります |
| stop.bat      | EMSウインドウズサービスを停止するスクリプト。 |
| uninstall.bat | EMSウインドウズサービスをアンインストールするスクリプト。 |



## Evo-Node アプリケーション

| Application Name | 内容                              |
| ---------------- | ---------------------------------------- |
| node-ews         | ファイルサービスやグループ名エイリアスやauthproxyなどのEMSに特定のコールのためのファイルが含まれています。 |
| node-webservices | Amazon S3やStreamロードバランサーへHLSファイルをアップロードするといったwebサービス用のファイルが含まれています。 |
| node-webui       | EMS Web UIのファイルが含まれています。 |



## 設定ファイル

| ファイル名           | 内容                              |
| ------------------- | ---------------------------------------- |
| auth.xml            | users.luaの設定ファイル          |
| bandwidthlimits.xml | サーバーが使用可能な最大帯域幅が定義されています。 |
| config.lua          | EMSの主要な設定ファイル |
| connlimits.xml      | EMSが許容する最大同時接続最大数が定義されています。 |
| ingestpoints.xml    | インジェストポイントの定義ファイル |
| pushPullSetup.xml   | EMSがランタイムAPIによりコマンド実行されたストリームアクションコマンドを保存しているファイル。本ファイルをマニュアルで編集する必要はありません。ファイルに変更があるとEMSはスタートアップ時に検出し、本ファイルを別名保存して、空白・新規で本ファイルが再作成され適用されます。 |
| users.lua           | ストリームがEMSにプッシュされる際の認証定義 |
| webconfig.json      | EvoStream Web Server (EWS) 設定ファイル |



## ドキュメント

| ファイル名                          | 内容                              |
| ---------------------------------- | ---------------------------------------- |
| EvoStream Media Server EULA v2.pdf | EMSエンドユーザ使用許諾契約 |



## その他

| ファイル/フォルダ名       | 内容                              |
| ---------------------- | ---------------------------------------- |
| blacklist.txt          | ブラックリストIPアドレスのリスト |
| whitelist.txt          | ホワイトリストIPアドレスのリスト |
| server.key             | セキュリティ認証に使用するプライベートキー |
| server.cert            | セキュリティ認証の証明書 |
| tests.exe              | Windows用のテストアプリケーション |
| platformTests          | Linux用のテストアプリケーション |
| media/                 | mediaディレクトリはビデオオンデマンド用ファイルのデフォルトの保存場所です。VODリクエストがあるとEMSはここを見に行きます。デフォルトの保存場所は`/config/config.lua`ファイルを編集することにより変更が可能です。 |
| logs/                  | EMSおよびEvoWebserverがログを保存するディレクトリです。デフォルトの保存場所はconfig.luaのEMS logsおよびWebconfig.jsonの項で変更が可能です。 |
| License.lic            | EMSを実行するために必要となるライセンスファイルです。 `config/` または `bin/` または `/etc/evostreamms/` またはevostreammsのバイナリがある場所のいずれかに置いても有効です。 |
| /node-webservices/logs | node-webservicesのログの保存ディレクトリです |
| /node-webui/logs       | node-webuiログの保存ディレクトリです   |
