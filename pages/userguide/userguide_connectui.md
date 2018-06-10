---
title: Connecting to Web UI
sidebar: userguide_sidebar
permalink: userguide_connectui.html
folder: userguide
toc: true
---

## 自動スタートアップ

EMS起動の際、config.luaファイルの`rubWebUI`が`true`に設定されている場合、EMS Web UIも同時に起動します。ブラウザでUIを確認することができます:


```
書式: <EMS_IP>:<WebUI_Port>

例: localhost:4100
```



## 手動スタートアップ

config.luaファイルの`rubWebUI`が`false`に設定されている場合も下記の方法でUIを実行することはできます:



### コンソール経由

`run_console_webui`を使うとWeb UIが別コンソールで開始します。Web UIからのログを個別に確認したい場合に有用です。


1. Linuxでは`run_console_webui.sh`を、ウインドウズでは`run_console_webui.bat`を実行する

   ![](images/userguide/startui_console.jpg)

   ​

2. ブラウザでUIを開く:

   ```
   書式: <EMS_IP>:<WebUI_Port>

   例: localhost:4100
   ```


​      **Note:**

   - `../node-webui/config/logging.json`を編集することでログレベル設定が可能です。




### デーモン経由

Linux環境のみですが、Web UIをデーモンモードで実行することが可能です。Web UIのアクティビティについてのログはコンソール上で表示しません。


1. `run_daemon_webui.sh`を実行します

2. ブラウザでUIを開く:

   ```
   書式: <EMS_IP>:<WebUI_Port>

   例: localhost:4100
   ```

   **Notes:**

   - `ps -ef|grep node`でWeb UIの実行状況を確認できます。 結果に`./evo-node node-webui/bin/webui_activate`と表示されるはずです。
   - `../node-webui/logs/`でWeb UIログを確認できます。
   - ログレベル設定はコンソールログやファイルログと同様です

   ​




## Web UIの停止

`run_console_webui.bat`、`run_console_webui.sh`、`run_daemon_ems.sh`のいずれかでUIを実行した場合:

1. ウインドウズでは`run_stop_webui.bat` Linuxでは`run_stop_webui.sh` を実行することで停止します

   ```
   $ ./run_stop_webui.sh
   webui will now be stopped
   ```

Web UIプロセスの実行を停止します
