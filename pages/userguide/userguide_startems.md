---
title: Starting EvoStream Media Server
keyword: start ems
sidebar: userguide_sidebar
permalink: userguide_startems.html
folder: userguide
toc: true
---



## Linux ディストリビューション (Linux apt/yum インストーラー)

EMSサービスとして実行するには:

```
# service evostreamms start
```
かまたは
```
# service evostreamms start_console
```

**上記２つの違いについて** `start_console`の場合はEMSのログはコンソール上に表示されます。`start` の場合はコンソールにはログは表示されません。

EMSを再起動するには:

```
# service evostreamms restart
```





## Linux, Mac OSX および BSD ディストリビューション (.tar.gz ディストリビューション)

EvoStream Media Serverを起動するために使う２つの"run~"スクリプトがあります。EMSの`./bin`フォルダ以下にあります:

1. コンソールログありのEMSの起動。`./config/config.lua`がサーバー設定に使用されます

   ```
    $ ./run_console_ems.sh
   ```

2. EMSをバックグラウンドプロセスとして起動します。実行プロセスは`evostream`ユーザーに割当てようとします。

   ```
    $ ./run_daemon_ems.sh

   ```

**Notes:**

- どちらのコマンドも直接実行可能です。

- `run_daemon_ems.sh`で実行の際に`evostream`ユーザーが存在しない場合、エラーが表示されるものの、EMSはおそらく起動されています。 サーバーが起動しているかどうか確認するには、ターミナルで `ps –e | grep evo` を実行してください。以下のような結果が表示されます:

  ```
  user@ubuntu:~$ ps –e|grep evo
  10727 pts/4 00:00:22 evostreamms
  10728 pts/4 00:00:05 evo-node (for webserver)
  10729 pts/4 00:00:00 evo-node (for webui)
  10730 pts/4 00:00:00 evo-node (for webservices)
  ```

OSによって、結果表示は若干異なりますが、サーバーが起動しているかどうかの確認はできます。

- **ユーザー** はスクリプト実行時`-u` オプション指定により変更可能です
- EvoStream Media Serverを実行するユーザーは、ネットワークportをopenしたりbindできるよう適切なパーミッションが必要です。




## Windows ディストリビューション

EMSはウインドウズの**Windows Services**を使って起動することができます

### サービス

**事前準備:**

ウインドウズレジストリでEMSサービスを有効化しておく必要があります。

1. コマンドプロンプトを開き

2. `C:\EvoStream\services\ems` サービスフォルダを選択し

3. `create.bat`コマンドに送り込みます

   ```
   C:\EvoStream\services\ems> create.bat
   ```
   **Note:** バッチファイルをダブルクリックしても実行できます

   ​

4. 確認を求められますので **Yes** ボタンをクリックしてください。

  ![](images/userguide/register.JPG)

  ​

5. EMS keysが登録されました **OK** をクリックしてください。

  ![](images/userguide/register_success.JPG)

  ​

6. `Control Panel > Administrative  Tools > Services`から登録の確認ができます。

  ![](images/userguide/registry_services.jpg)



**サービスの開始**

1. コマンドプロンプトを開き

2. `C:\EvoStream\services\ems`フォルダに

3. `start.bat`コマンドを送り込みます

   サービスが開始されます

   ​


**Notes:**

- EMSサービスの停止は `stop.bat` をCallします
- `remove.bat` コマンドでEMSのレジストリ登録を削除できます





### ショートカットアイコン経由での起動

インストール時にショートカットを作成しておくことで、ショートカット経由でEMSを起動することもできます。

 ![](images/home/startupicon.JPG)

EMSをコンソール起動します。

ショートカットは`run_console_ems.bat`を呼び出します。EMSがインストールされているディレクトリで直接ダブルクリックしてサーバーを起動することもできます。このスクリプトはメディアサーバーをコマンドプロンプトで起動し、サーバー設定には`config/config.lua`を使用します。



```
C:\EvoStream\run_console_ems.bat
```



## 起動の確認

ウインドウズやLinux/BSD/OSXにおいてEMSをコンソールアプリケーションとして起動した場合、サーバーが起動したことを示す次の表示となります


![](images/userguide/start1.png)

**Tip!** EMSが正常に起動するとコンソールに GO! GO! GO!と表示されます。

起動したアプリケーションはタスクマネージャーで確認できます。

```
evostreamms.exe
evo-node.exe    (webserver)
evo-node.exe    (webui)
evo-node.exe    (webservices)
```





## EMS コマンドライン定義

いくつかのコマンドラインオプションが使用できます

**Format:** evostreamms [オプション][configファイルのパス]

| コマンド                          | 機能                                 |
| -------------------------------- | ---------------------------------------- |
| `–help`                          | ヘルプを表示します               |
| `–version`                       | バージョン情報を表示します             |
| `–use-implicit-console-appender` | 実行時エキストラログを記録します。コンソールアプリケーションとして起動された場合にのみ有効です。サーバーが起動してすぐに停止してしまう場合に原因の切り分けに有効です。 |
| `–daemon`                        | 設定ファイルのデーモン設定内容を無視し、デーモンモードでサーバーを起動します |
| `–uid=`                          | 指定したユーザーidでプロセスを実行します |
| `–gid=`                          | 指定したグループidでプロセスを起動します |
| `–pid=<pid_file>`                | PIDファイルを生成します。-daemonオプションと一緒に使う必要があります |

------

## Notes

- EMSを起動すると下記の項目も同時に起動します:

  - EMS Web Server
  - EMS Web UI
  - EMS Webservices

- config.luaで起動プロセスを設定することができます

  - [runWebServer](userguide_configlua.html#runwebserver)

  - [runWebUI](userguide_configlua.html#runwebui)

  - [eventLogger](userguide_configlua.html#eventlogger)

    ​
