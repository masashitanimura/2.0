---
title: Installation on Linux OS
sidebar: userguide_sidebar
permalink: userguide_installlinuxos.html
folder: userguide
toc: true
---



## プラットフォームの確認

ご使用のOSに適切なディストリビューションをダウンロードされたかを確認するには、`platformTests` プログラムをご利用ください。このプログラムはすべてのディストリビューションに含まれており、binディレクトリ下にあります。互換性に関するテストを行います。


コンソールまたはターミナルを開き、`platformTests`を実行します (`./platformTests`)
プラットフォーム互換性テスト結果を表示します。テストにパスしたら、適切なディストリビューションということです。



## Linuxの制限

Linuxシステムはデフォルトでプロセスが使用可能なソケット数およびファイルディスクリプタ数に制限を設けており、
これはEMSについても当てはまります。サーバーが扱うコネクション数が1024を越えることが予測されているなら、`/etc/security/limits.conf` 設定ファイルを編集する必要があります。

次のように追加・変更する必要があります。

```
soft nofile 16384
hard nofile 65536
soft nproc 4096
hard nproc 16384
```

## インストールの手順

### Linuxパッケージ (Linux apt/yum インストーラー)

#### 事前準備:

- keyファイルがダウンロードできるようファイルーウォールの制限を無効にしてください

- インストールには管理者権限が必要となります

  sudo ユーティリティが使える場合

  ```
  $ su –
  ```

  sudo ユーティリティが使えない場合

  ```
  $ sudo su –
  ```

  **Note:** 管理者権限が有効になるとコマンドプロンプトが `$` から `#` に変わります。



#### インストール手順:

EvoStreamソフトウェアリポジトリをインストールするためのスクリプトをダウンロードします

- DebianベースのLinuxディストリビューションの場合 (Ubuntu または Debian)

  ```
  # wget http://apt.evostream.com/installkeys.sh -O /tmp/installkeys.sh
  ```

- RedHatベースのLinuxディストリビューションの場合 (CentOS, Fedora, RHEL)

  ```
  # curl http://yum.evostream.com/installkeys.sh -o /tmp/installkeys.sh
  ```

  ​

2\. EvoStream software repositoryおよびkeysのインストールを行うためにスクリプトを実行してください

```
# sh /tmp/installkeys.sh
```

- 実行がうまくいった場合、下記のようなメッセージが表示されます:

  ```
  "EvoStream keys installed successfully"
  ```

EvoStreamソフトウェアリポジトリおよびkeysのインストールが完了したことになります。パッケージのインストールに進んでください。



**Note:** 手順１および２の実行は１回のみとしてください

EvoStream Media Serverのインストールは以下の手順です。この手順はEMSのアップデートの際も同様です。



3\. EvoStream Media Serverのインストール.

- DebianベースのLinuxディストリビューション (Ubuntu または Debian)

  ```
  # apt-get install evostream-mediaserver
  ```

- RedHatベースのLinuxディストリビューション (CentOS, Fedora, RHEL)

  ```
  # yum install evostream-mediaserver
  ```




#### ライセンスのインストール

ライセンスのインストールは `License.lic` ファイルを `/etc/evostreamms/` 以下にコピーするだけです。




### Linuxアーカイブ版 (.tar.gzディストリビューション)

アーカイブ版(.tar.gz)のEMSをインストールすることも可能です。最新のリリースはEvoStream ウェブサイト: [https://evostream.com/software-downloads/](https://evostream.com/software-downloads/)からダウンロード可能です。

ご利用のOSに適したディストリビューションを選択いただく必要があります。

ダウンロードしたEMSパッケージを伸長・展開してください。インストールするパスに特に制限はありませんが、セキュリティの観点からweb-rootにはインストールしないことをおすすめします。


#### ライセンスのインストール

ライセンスのインストールは `License.lic` ファイルを `../config/evostreamms/` 以下にコピーするだけです。



## ディストリビューション内容

### Linuxパッケージ

**A. 設定ファイル **

```
├── etc
│   └── evostreamms
│       ├── blacklist.txt
│       ├── config.lua
│       ├── server.cert
│       ├── server.key
│       ├── users.lua
│       ├── webconfig.lua
│       └── whitelist.txt
```

**B. 実行およびノードファイル**

```
├── usr
│   ├── bin
│   │   ├── evo-avconv
│   │   ├── evo-mp4writer
│   │   ├── evo-node
│   │   ├── evostreamms
│   │   ├── node-ews
│   │   ├── node-webservices
│   │   ├── node-webui
│   └── share
│       ├── evo-avconv
│       │   └── presets
│       │       ├── libx264-baseline.avpreset
│       |       ├── libx264-fast.avpreset
│       |       ├── libx264-fast.avpreset
│       |       ├── libx264-faster.avpreset
│       |       ├── libx264-faster.avpreset
│       |       ├── libx264-ipod320.avpreset
│       |       ├── libx264-ipod640.avpreset
│       |       ├── libx264-lossless_fast.avpreset
│       |       ├── libx264-lossless_max.avpreset
│       |       ├── libx264-lossless_medium.avpreset
│       |       ├── libx264-lossless_slow.avpreset
│       |       ├── libx264-lossless_slower.avpreset
│       |       ├── libx264-lossless_ultrafast.avpreset
│       |       ├── libx264-main.avpreset
│       |       ├── libx264-medium.avpreset
│       |       ├── libx264-medium_firstpass.avpreset
│       |       ├── libx264-placebo.avpreset
│       |       ├── libx264-placebo_firstpass.avpreset
│       |       ├── libx264-slow.avpreset
│       |       ├── libx264-slow_firstpass.avpreset
│       |       ├── libx264-slower.avpreset
│       |       ├── libx264-slower_firstpass.avpreset
│       |       ├── libx264-superfast.avpreset
│       |       ├── libx264-superfast_firstpass.avpreset
│       |       ├── libx264-ultrafast.avpreset
│       |       ├── libx264-ultrafast_firstpass.avpreset
│       |       ├── libx264-veryfast.avpreset
│       |       ├── libx264-veryfast_firstpass.avpreset
│       |       ├── libx264-veryslow.avpreset
│       |       └── libx264-veryslow_firstpass.avpreset
│       └── doc
│           └── evostreamms
│               ├── copyright
│               ├── EvoStream Media Server EULA v2.pdf
│               ├── README.txt
│               └── version
│                   ├── BUILD_DATE
│                   ├── BUILD_NUMBER
│                   ├── CODE_NAME
│                   ├── OS_NAME
│                   ├── OS_VERSION
│                   └── RELEASE_NUMBER
```

**B.1. Node-WebServerファイル**

```
├── usr
│   ├── bin
│   │   ├── node-ews
│   │   |   ├── evo-phpengine
│   │   |   ├── ews.node
│   │   |   ├── fileRotateSize.js
│   │   |   ├── helper.js
│   │   |   ├── node-ews.js
│   │   |   ├── node_modules
│   │   │   |   ├── basic-auth
│   │   │   |   ├── connect
│   │   │   |   └── winston
│   │   |   └── req_handlers     
│   │   │   |   ├── authproxy.js
│   │   │   |   ├── default.js
│   │   │   |   ├── httpstream.js
│   │   │   |   ├── php.js
│   │   │   |   └── resphdrs.js  
```

**B.2. Node-Webservicesファイル**

```
├── usr
│   ├── bin
│   │   ├── node-webservices
│   │   |   ├── app.js
│   │   |   ├── base_plugins
│   │   │   |   ├── basehdsplugin.js
│   │   │   |   ├── basehlsplugin.js
│   │   │   |   └── baseplugin.js    
│   │   |   ├── bin
│   │   │   |   └── www       
│   │   |   ├── config
│   │   │   |   ├── logging.json
│   │   │   |   └── plugins.json    
│   │   |   ├── core_modules
│   │   │   |   └── ems-api-core.js      
│   │   |   ├── LICENSE
│   │   |   ├── logs
│   │   │   |   └── evowebservices.log          
│   │   |   ├── node_modules
│   │   │   |   ├── body-parser
│   │   │   |   ├── comment-json
│   │   │   |   ├── concat-stream
│   │   │   |   ├── debug
│   │   │   |   ├── express
│   │   │   |   ├── morgan
│   │   │   |   ├── request-enhanced
│   │   │   |   ├── s3
│   │   │   |   └── winston
│   │   |   ├── package.json
│   │   |   ├── plugins
│   │   │   |   ├── amazondashupload.js
│   │   │   |   ├── amazonhdsupload.js
│   │   │   |   ├── amazonhlsupload.js
│   │   │   |   ├── streamautorouter.js
│   │   │   |   ├── streamloadbalancer.js
│   │   │   |   └── streamrecorder.js   
│   │   |   ├── README.md
│   │   |   ├── README.txt
│   │   |   ├── routes
│   │   │   |   ├── evowebservices.js
│   │   │   |   └── index.js      
│   │   |   ├── services
│   │   │   |   └── plugin-service.js
│   │   |   ├── views
│   │   │   |   ├── error.hbs
│   │   │   |   ├── index.hbs
│   │   │   └── └── layout.hbs
```

**B.3. Node-WebUI ファイル**

```
├── usr
│   ├── bin
│   │   ├── node-webui
│   │   |   ├── app.js
│   │   |   ├── auth
│   │   │   │   ├── passport-config.js
│   │   │   │   └── restrict.js
│   │   |   ├── bin
│   │   │   │   └── webui_activate
│   │   |   ├── config
│   │   │   │   ├── dir-config.js
│   │   │   │   ├── logging.json
│   │   │   │   └── social-auth-config.js
│   │   |   ├── core_modules
│   │   │   │   ├── ems-api-core.js
│   │   │   │   ├── ems-api-proxy.js
│   │   │   │   ├── ems-config-core.js
│   │   │   │   └──  socket-io-api.js
│   │   |   ├── data
│   │   │   │   ├── help.json
│   │   │   │   └──  user.json   
│   │   |   ├── logs
│   │   │   │   ├── webui.log
│   │   |   ├── models
│   │   │   │   ├── list-config.js
│   │   │   │   ├── list-streams.js
│   │   │   │   └──  user.js
│   │   |   ├── node_modules
│   │   │   │   └──  [168 node_module files]
│   │   |   ├── public
│   │   │   │   ├── css
│   │   │   │   ├── fonts
│   │   │   │   ├── images
│   │   │   │   ├── js
│   │   │   │   └──  media
│   │   |   ├── routes
│   │   │   │   ├── api-explorer.js   
│   │   │   │   ├── dashboard.js
│   │   │   │   ├── ems.js
│   │   │   │   ├── index.js
│   │   │   │   ├── tream.js
│   │   │   │   └── users.js
│   │   |   ├── services
│   │   │   │   └──  stream-service.js
│   │   |   ├── views
│   │   │   │   ├── admin
│   │   │   │   ├── index
│   │   │   │   ├── error.hbs
│   │   │   └── └──  index.hbs  
```

**4. XML ファイル**

```
└── var
    ├── evostreamms
    │   ├── media
    │   └── xml
    │       ├── auth.xml
    │       ├── bandwidthlimits.xml
    │       ├── connlimits.xml
    │       ├── ingestpoints.xml
    │       └── pushPullSetup.xml
```

**5. Evo-Webroot ファイル**

```
└── var
    ├── evo-webroot
    │   ├── demo
    │   │   ├── css
    │   │   ├── evoplayers.html
    │   │   ├── evo.png
    │   │   ├── evowsabrvideo.html
    │   │   ├── js
    │   │   │   └── evohtml5player-latest.bundle.js
    │   │   ├── jsonMetaTest.html
    │   │   ├── jsonMetaWriteTest.html
    │   │   └── loading.gif
    │   ├── clientaccesspolicy.xml
    │   └── crossdomain.xml    
```

**6. Log ファイル**

```
└── var
    ├── log
    │   └── evostreamms
```

**7. 実行ファイル**

```
└── var
    └── run
        └── evostreamms
```





### Linux Archive

```
./EvoStream Archive
  ├── bin
  │   ├── node-evowebservices
  │   │   ├── base_plugins
  │   │   │	  ├── basehdsplugin.js
  │   │   │	  ├── basehlsplugin.js
  │   │   │	  └── baseplugin.js    
  │   │   ├── bin
  │   │   │   └── www       
  │   │   ├── config
  │   │   │	  ├── logging.json
  │   │   │	  └── plugins.json    
  │   │   ├── core_modules
  │   │   │	  └── ems-api-core.js       
  │   │   ├── logs
  │   │   │	  └── evowebservices.log          
  │   │   ├── node_modules
  │   │   │	  ├── body-parser
  │   │   │	  ├── comment-json
  │   │   │	  ├── concat-stream
  │   │   │	  ├── debug
  │   │   │   ├── express
  │   │   │   ├── morgan
  │   │   │	  ├── request-enhanced
  │   │   │	  ├── s3
  │   │   │	  └── winston
  │   │   ├── plugins
  │   │   │	  ├── amazondashupload.js
  │   │   │	  ├── amazonhdsupload.js
  │   │   │	  ├── amazonhlsupload.js
  │   │   │	  ├── streamautorouter.js
  │   │   │	  ├── streamloadbalancer.js
  │   │   │	  └── streamrecorder.js   
  │   │   ├── routes
  │   │   │	  ├── evowebservices.js
  │   │   │	  └── index.js      
  │   │   ├── services
  │   │   │	  └── plugin-service.js
  │   │   ├── views
  │   │   │   ├── error.hbs
  │   │   │	  ├── index.hbs
  │   │   │	  └── layout.hbs
  │   │   ├── app.js
  │   │   ├── LICENSE
  │   │   ├── package.json
  │   │   ├── README.md
  │   ├── └── README.txt  
  │   ├── node-ews
  │   │   ├── node_modules
  │   │   │   ├── basic-auth
  │   │   │   ├── connect
  │   │   │   └── winston
  │   │   ├── req_handlers
  │   │   │   ├── authproxy.js
  │   │   │   ├── default.js
  │   │   │   ├── httpstream.js
  │   │   │   ├── php.js
  │   │   │   └── resphdrs.js  
  │   │   ├── evo-phpengine.exe
  │   │   ├── ews.node
  │   │   ├── fileRotateSize.js
  │   │   ├── helper.js
  │   │   └── node-ews.js
  │   ├── node-webui
  │   │   ├── auth
  │   │   │   ├── passport-config.js
  │   │   │   └── restrict.js
  │   │   ├── bin
  │   │   │   └── webui_activate
  │   │   ├── config
  │   │   │   ├── dir-config.js
  │   │   │   ├── logging.json
  │   │   │   └── social-auth-config.js
  │   │   ├── core_modules
  │   │   │   ├── ems-api-core.js
  │   │   │   ├── ems-api-proxy.js
  │   │   │   ├── ems-config-core.js
  │   │   │   └── socket-io-api.js
  │   │   ├── data
  │   │   │   ├── help.json
  │   │   │   └── user.json   
  │   │   ├── logs
  │   │   │   └── webui.log
  │   │   ├── models
  │   │   │   ├── list-config.js
  │   │   │   ├── list-streams.js
  │   │   │   └── user.js
  │   │   ├── node_modules
  │   │   │   └── [168 node_module files]
  │   │   ├── public
  │   │   │   ├── css
  │   │   │   ├── fonts
  │   │   │   ├── images
  │   │   │   ├── js
  │   │   │   └── media
  │   │   ├── routes
  │   │   │   ├── api-explorer.js   
  │   │   │   ├── dashboard.js
  │   │   │   ├── ems.js
  │   │   │   ├── index.js
  │   │   │   ├── stream.js
  │   │   │   └── users.js
  │   │   ├── services
  │   │   │   └── stream-service.js
  │   │   ├── views
  │   │   │   ├── admin
  │   │   │   ├── index
  │   │   │   ├── error.hbs
  │   │   │   └── index.hbs  
  │   │   ├── app.js
  │   │   ├── LICENSE
  │   │   └── package.json     
  │   ├── emsTranscoder.sh
  │   ├── evo-avconv
  │   ├── evo-mp4writer
  │   ├── evostreamms
  │   ├── platformTests
  │   ├── run_console_ems.sh
  │   ├── run_console_webui.sh
  │   ├── run_daemon_ems.sh
  │   ├── run_daemon_webui.sh  
  │   └── run_stop_webui.sh
  ├── config
  │   ├── auth.xml
  │   ├── bandwidthlimits.xml
  │   ├── blacklist.txt
  │   ├── config.lua
  │   ├── connlimits.xml
  │   ├── ingestpoints.cml
  │   ├── pushPullSetup.xml
  │   ├── server.cert
  │   ├── server.key
  │   ├── users.lua
  │   ├── webconfig.json
  │   └── whitelist.txt
  ├── evo-avconv-presets
  │   └── [30 transcode preset files]
  ├── evo-webroot
  │   ├── demo
  │   │   ├── css
  │   │   │   ├── common.css
  │   │   │	  └── common.css.orig  
  │   │   ├── js
  │   │   │	  └── evohtml5player-latest.bundle.js
  │   │   ├── evo.png
  │   │   ├── evoplayers.html
  │   │   ├── evowsabrvideo.html
  │   │   ├── jsonMetaTest.html
  │   │   ├── jsonMetaWriteTest.html
  │   │   └── loading.gif
  │   ├── clientaccesspolicy.xml
  │   └── crossdomain.xml
  ├── logs
  ├── media
  ├── BUILD_DATE
  ├── Evostream Media Server EULA v2.pdf
  └── README.txt
```
