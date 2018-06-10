---
title: Installation on Windows OS
sidebar: userguide_sidebar
permalink: userguide_installwinos.html
folder: userguide
toc: true
---


## インストール手順

1. [https://evostream.com/software-downloads](https://evostream.com/software-downloads)からEMSパッケージインストーラーをダウンロードしてください

2. EMSのインストール

   2.1. zipパッケージを伸長・展開します

   2.2. `setup.exe`を右クリックし管理者として実行をクリックしてください

   ![](images/userguide/qsgfw1.jpg)

   ​

   2.3. 言語を選択し**OK**ボタンをクリックしてください

   ![](images/userguide/qsgfw2.jpg)

   ​

   2.4. **Next**ボタンをクリックしインストールを続行してください

   ![](images/userguide/qsgfw3.jpg)

   ​

   2.5 ライセンス使用許諾文書を確認し **I accept the agreement**ボタンをクリックし **Next**をクリックしてください

   ![](images/userguide/qsgfw4.jpg)

   ​

   2.6. インストール先のパスを確認し、 **Next**ボタンをクリックしてください。

   ![](images/userguide/qsgfw5.jpg)

   ​

   2.7.  **Create a desktop icon**にチェックを入れ **Next**ボタンをクリックしてください

   ![](images/userguide/qsgfw6.jpg)

   ​

   2.8. **Install**ボタンをクリックしてください

   ![](images/userguide/qsgfw7.jpg)

   ​

   2.9. informationを参照し、**Next**ボタンをクリックしてください

   ![](images/userguide/qsgfw8.jpg)

   ​

   2.10.  **Finish**ボタンをクリックしインストールを完了してください

   ![](images/userguide/qsgfw9.jpg)

   ​

   **Note:** ライセンスファイルを未だインストールしていない場合は、 **Launch EMS**のチェックを外して、**Finish**ボタンをクリックしてください。






## ラインセンスのインストール

**Note:** ライセンスファイルをお手元にご用意ください。30日間の試用版をお試しになりたい場合は、
[here]をクリックし(https://evostream.com/free-trial/)必要事項を記入しリクエストしてください。
その他のライセンスの購入に関するお問い合わせは[salesupport@evostream](mailto:salessupport@evostream.com) まで

ライセンスをインストールするには `License.lic` ファイルを `C:\EvoStream\config` 以下にコピーするだけです。





## 配布内容

```
C:\EvoStream
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
   │   ├── libx264-baseline.avpreset
   │   ├── libx264-fast.avpreset
   │   ├── libx264-fast.avpreset
   │   ├── libx264-faster.avpreset
   │   ├── libx264-faster.avpreset
   │   ├── libx264-ipod320.avpreset
   │   ├── libx264-ipod640.avpreset
   │   ├── libx264-lossless_fast.avpreset
   │   ├── libx264-lossless_max.avpreset
   │   ├── libx264-lossless_medium.avpreset
   │   ├── libx264-lossless_slow.avpreset
   │   ├── libx264-lossless_slower.avpreset
   │   ├── libx264-lossless_ultrafast.avpreset
   │   ├── libx264-main.avpreset
   │   ├── libx264-medium.avpreset
   │   ├── libx264-medium_firstpass.avpreset
   │   ├── libx264-placebo.avpreset
   │   ├── libx264-placebo_firstpass.avpreset
   │   ├── libx264-slow.avpreset
   │   ├── libx264-slow_firstpass.avpreset
   │   ├── libx264-slower.avpreset
   │   ├── libx264-slower_firstpass.avpreset
   │   ├── libx264-superfast.avpreset
   │   ├── libx264-superfast_firstpass.avpreset
   │   ├── libx264-ultrafast.avpreset
   │   ├── libx264-ultrafast_firstpass.avpreset
   │   ├── libx264-veryfast.avpreset
   │   ├── libx264-veryfast_firstpass.avpreset
   │   ├── libx264-veryslow.avpreset
   │   └── libx264-veryslow_firstpass.avpreset
   ├── evo-webroot  
   │   ├── demo
   │   │   ├── css
   │   │   │	├── common.css
   │   │   │	└── common.css.orig  
   │   │   ├── js
   │   │   │	└── evohtml5player-latest.bundle.js
   │   │   ├── evo.png
   │   │   ├── evoplayers.html
   │   │   ├── evowsabrvideo.html
   │   │   ├── jsonMetaTest.html
   │   │   ├── jsonMetaWriteTest.html
   │   │   └── loading.gif
   │   ├── clientaccesspolicy.xml
   │   └── crossdomain.xml   
   ├── node-evowebservices
   │   │   ├── base_plugins
   │   │   │	├── basehdsplugin.js
   │   │   │	├── basehlsplugin.js
   │   │   │	└── baseplugin.js    
   │   │   ├── bin
   │   │   │	└── www       
   │   │   ├── config
   │   │   │	├── logging.json
   │   │   │	└── plugins.json    
   │   │   ├── core_modules
   │   │   │	└── ems-api-core.js       
   │   │   ├── logs
   │   │   │	└── evowebservices.log          
   │   │   ├── node_modules
   │   │   │	├── body-parser
   │   │   │	├── comment-json
   │   │   │	├── concat-stream
   │   │   │	├── debug
   │   │   │	├── express
   │   │   │	├── morgan
   │   │   │	├── request-enhanced
   │   │   │	├── s3
   │   │   │	└── winston
   │   │   ├── plugins
   │   │   │	├── amazondashupload.js
   │   │   │	├── amazonhdsupload.js
   │   │   │	├── amazonhlsupload.js
   │   │   │	├── streamautorouter.js
   │   │   │	├── streamloadbalancer.js
   │   │   │	└── streamrecorder.js   
   │   │   ├── routes
   │   │   │	├── evowebservices.js
   │   │   │	└── index.js      
   │   │   ├── services
   │   │   │	└── plugin-service.js
   │   │   ├── views
   │   │   │	├── error.hbs
   │   │   │	├── index.hbs
   │   │   │	└── layout.hbs
   │   │   ├── app.js
   │   │   ├── LICENSE
   │   │   ├── package.json
   │   │   ├── README.md
   │   └── └── README.txt
   ├── logs   
   ├── media
   ├── node-ews
   │   ├── ext
   │   │   └── php_curl.dll
   │   ├── node_modules
   │   │   ├── basic-auth
   │   │   ├── connect
   │   │   └── winston
   │   ├── req_handlers
   │   │   ├── authproxy.js
   │   │   ├── default.js
   │   │   ├── httpstream.js
   │   │   ├── php.js
   │   │   └── resphdrs.js  
   │   ├── evo-phpengine.exe
   │   ├── ews.node
   │   ├── fileRotateSize.js
   │   ├── helper.js
   │   ├── node-ews.js
   │   ├── php.ini
   │   └── php5ts.dll
   ├── node-webui
   │   ├── auth
   │   │   ├── passport-config.js
   │   │   └── restrict.js
   │   ├── bin
   │   │   └── webui_activate
   │   ├── config
   │   │   ├── dir-config.js
   │   │   ├── logging.json
   │   │   └── social-auth-config.js
   │   ├── core_modules
   │   │   ├── ems-api-core.js
   │   │   ├── ems-api-proxy.js
   │   │   ├── ems-config-core.js
   │   │   └── socket-io-api.js
   │   ├── data
   │   │   ├── help.json
   │   │   └── user.json   
   │   ├── logs
   │   │   └── webui.log
   │   ├── models
   │   │   ├── list-config.js
   │   │   ├── list-streams.js
   │   │   └── user.js
   │   ├── node_modules
   │   │   └── [168 node_module files]
   │   ├── public
   │   │   ├── css
   │   │   ├── fonts
   │   │   ├── images
   │   │   ├── js
   │   │   └── media
   │   ├── routes
   │   │   ├── api-explorer.js   
   │   │   ├── dashboard.js
   │   │   ├── ems.js
   │   │   ├── index.js
   │   │   ├── stream.js
   │   │   └── users.js
   │   ├── services
   │   │   └── stream-service.js
   │   ├── views
   │   │   ├── admin
   │   │   ├── index
   │   │   ├── error.hbs
   │   │   └── index.hbs  
   │   ├── app.js
   │   ├── LICENSE
   │   └── package.json   
   ├── services
   │   ├── ems
   │   │   ├── create.bat
   │   │   ├── remove.bat
   │   │   ├── start.bat   
   │   │   ├── stop.bat      
   │   │   └── uninstall.bat    
   │   └── nssm.exe   
   ├── emsTranscoder.bat
   ├── evo-avconv.exe
   ├── evo-mp4writer.exe
   ├── evo-node.exe
   ├── Evostream Media Server EULA v2.pdf
   ├── evostreamms.exe
   ├── evo-webserver.exe
   ├── libgcrypt-20.dll
   ├── libgmp-10.dll
   ├── libgnutls-28.dll
   ├── libgpg-error6-0.dll
   ├── libhogweed-2-5.dll
   ├── libiconv-2.dll
   ├── libmicrohttpd-12.dll
   ├── libnettle-4-7.dll
   ├── README.txt
   ├── run_console_ems.bat
   ├── run_console_webui.bat
   ├── tests.exe
   ├── unins000.dat
   ├── unins000.exe
   └── zlib1.dll
```
