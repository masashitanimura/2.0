---
title: whitelist.txt
keywords: whitelist
sidebar: userguide_sidebar
permalink: userguide_whitelist.html
folder: userguide
toc: false
---


EMSにアクセス可能なIPアドレスを定義します。ホワイトリストが定義されている場合、ファイルに記述されたIPアドレスのみアクセス可能です。

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

**Notes:**

- ホワイトリストファイルを読み込むにはwebconfig.luaで`enableIPFilter`は`true`に設定されている必要があります。

- ホワイトリストIPアドレスリストを有効にするためには`whitelistFile`コードはコメントしないようにしてください

  ```
    enableIPFilter=true,
    whitelistFile="..\\config\\whitelist.txt",
    blacklistFile="..\\config\\blacklist.txt",
  ```

- もしも特定のIPアドレスがホワイトリストとブラックリストの両方に存在する場合は、ブラックリストにあるものとして判定されます。



------

## 関連リンク

- [blacklist.txt](userguide_blacklist.html)
- [Blacklisting](userguide_blacklisting.html)
