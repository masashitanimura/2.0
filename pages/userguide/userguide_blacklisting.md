---
title: Blacklisting
sidebar: userguide_sidebar
permalink: userguide_blacklisting.html
folder: userguide
toc: false
---

ブラックリスト設定はEMSへのアクセスを制限するものです。制限はwebで使用されるポート（デフォルトは**8888**）へのアクセスに対して有効です。この機能は２つの設定ファイル（[blacklist.txt](userguide_blacklist.html) および [whitelist.txt](userguide_whitelist.html)）により構成されます



## 設定方法

1. webconfig.lua内でblacklistおよびwhitelistの設定が有効化されているか

   ```
   enableIPFilter=true,
   whitelistFile="..\\config\\whitelist.txt",
   blacklistFile="..\\config\\blacklist.txt",
   ```

   **Note**: `enableIPFilter`はデフォルトでfalseに設定されています

   ​

2. blacklist および whitelistテキストファイルにIPアドレスを追記する

   **例:**

   ***blacklist.txt***

   ```
   192.168.2.3
   192.168.2.4
   192.168.2.5
   192.168.2.6
   192.168.2.7
   192.168.2.8
   192.168.2.9
   192.168.2.10
   ```

   ***whitelist.txt***

   ```
   192.168.2.11
   192.168.2.12
   192.168.2.13
   ```

3. EMSを起動する

   この例ではwhitelist.txtに記載のあるipアドレスからのアクセスのみEMSのwebサーバーポートにアクセスすることができ、その他のアドレスからのアクセスは制限されます。実装は以下の通りです。


   **実装:**

   | ブラックリスト | ホワイトリスト | 許可されるIP                           |
   | :-------: | :-------: | -------------------------------------- |
   |   空白   |   空白   | すべてのIPが許可されます                      |
   |  x.x.x.x  |   空白    | x.x.x.x以外のIPが許可されます |
   |   空白    |  y.y.y.y  | y.y.y.yのみ許可されます              |
   |  x.x.x.x  |  y.y.y.y  | y.y.y.yのみ許可されます                |
   |  ファイルなし  |  y.y.y.y  | y.y.y.yのみ許可されます                |
   |  x.x.x.x  |  ファイルなし  | x.x.x.x以外のIPが許可されます |
   |  ファイルなし  |  ファイルなし  | エラーとなります                                  |


------

## Notes

- リストにIPv6を使用することも可能です

------

## 関連リンク

- [blacklist.txt](userguide_blacklist.html)
- [whitelist.txt](userguide_whitelist.html)
