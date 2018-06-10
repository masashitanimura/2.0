---
title: ingestpoints.xml
keywords: ingestpoints
sidebar: userguide_sidebar
permalink: userguide_ingestpoints.html
folder: userguide
toc: false
---

インジェストポイントの設定ファイルです。インジェストポイントを使用する場合はtrueに設定する必要があります。

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
</MAP>
```



config.luaで`hasIngestPoints`がtrueの場合、APIコールでインジェストが生成されます。

**API call:**

```
createIngestPoint privateStreamName=theIngestPoint1 publicStreamName=Stream1

createIngestPoint privateStreamName=theIngestPoint2 publicStreamName=Stream2

createIngestPoint privateStreamName=theIngestPoint3 publicStreamName=Stream3

createIngestPoint privateStreamName=theIngestPoint4 publicStreamName=Stream4

createIngestPoint privateStreamName=theIngestPoint5 publicStreamName=Stream5
```



**ingestpoints.xml**

```
<?xml version="1.0" ?>
<MAP isArray="true" name="">
    <STR name="theIngestPoint1">Stream1</STR>
    <STR name="theIngestPoint2">Stream2</STR>
    <STR name="theIngestPoint3">Stream3</STR>
    <STR name="theIngestPoint4">Stream4</STR>
    <STR name="theIngestPoint5">Stream5</STR>
</MAP>
```
------

## 関連リンク

- [hasIngestPoints](userguide_configlua.html#hasingestpoints)
