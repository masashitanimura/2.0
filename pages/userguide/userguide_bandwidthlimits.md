---
title: bandwidthlimits.xml
keywords: bandwidthlimits
sidebar: userguide_sidebar
permalink: userguide_bandwidthlimits.html
folder: userguide
toc: false
---

サーバーが使用する最大帯域の設定を定義します(一時的帯域キャップ)

config.luaで`enableCheckBandwidth`がtrueの場合、EMSはbandwidths.xmlファイルを読み込み、入出力両方のストリームにおける総帯域を設定値に制限します。

入出力ともにデフォルト値はゼロ(0)で、無制限という意味です。


```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <DOUBLE name="in">0.000</DOUBLE>
    <DOUBLE name="out">0.000</DOUBLE>
</MAP>
```

 [enableCheckBandwidth](userguide_configlua.html#enablecheckbandwidth)を見る
