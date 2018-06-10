---
title: blacklist.txt
keywords: blacklist
sidebar: userguide_sidebar
permalink: userguide_blacklist.html
folder: userguide
toc: false
---

EMSによりブロックされるIPアドレスの定義を行えます。ブラックリストが設定されている場合、ブラックリストに記述されたIPアドレスからのアクセスを拒否します。



**実装:**

| ブラックリスト | ホワイトリスト | 許可される IP                            |
| :-------: | :-------: | -------------------------------------- |
|   空白   |   空白   | すべてのIPが許可されます                    |
|  x.x.x.x  |   空白   | x.x.x.x以外のIPが許可されます |
|   空白   |  y.y.y.y  | y.y.y.yのみ許可されます                |
|  x.x.x.x  |  y.y.y.y  | y.y.y.yのみ許可されます              |
|  ファイルなし  |  y.y.y.y  | y.y.y.yのみ許可されます                     |
|  x.x.x.x  |  ファイルなし  | x.x.x.x以外のIPが許可されます |
|  ファイルなし  |  ファイルなし  | エラーとなります                                  |

------

##Notes:

- ブラックリストファイルを読み込むにはwebconfig.luaで`enableIPFilter`は`true`に設定されている必要があります。


- ブラックリストIPアドレスリストを有効にするためには`blacklistFile`コードはコメントしないようにしてください

  *config.lua内の記述:*

  ```
    enableIPFilter=true,
    whitelistFile="..\\config\\whitelist.txt",
    blacklistFile="..\\config\\blacklist.txt",
  ```

- もしも特定のIPアドレスがホワイトリストとブラックリストの両方に存在する場合は、ブラックリストにあるものとして判定されます。


------

## 関連リンク

- [whitelist.txt](userguide_whitelist.html)
- [Blacklisting](userguide_blacklisting.html)
