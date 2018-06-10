---
title: pushPullSetup.xml
keywords: pushPullSetup
sidebar: userguide_sidebar
permalink: userguide_pushPullSetup.html
folder: userguide
toc: false
---

pushPullSetup.xmlファイルはランタイムAPI経由でのストリームアクションコマンドを保存しておくのに使用されます。pushPullSetup.xmlファイルに関して最も重要なことはファイル内容を むやみに変更しないことです。このファイルは内部設定目的で使用されます。起動時にEMSがpushpullSetup.xmlファイルに変更があったと判断すると、ファイル名を変更し、新規の設定ファイルで起動が行われます。

本ファイルがどのように使用されるかを知ることは重要です。pullstream, pushstream, createHLDStream, createHDSStream, createMSSStream, createDASHStream, record, launchProcess, startWebRtcコマンド等が実行されると、本ファイルに記録されます(keepAliveフラグがデフォルト値の1の場合)。

EMSが起動されると本ファイルをパースし、記述された全ての接続を再生成しようとします。設定エントリは removeConfig コマンドを用いて削除することができますし、初回コマンドを実行する際にkeepAliveフラグを0に設定することでも記録を省略できます。


```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <STR name="checksum">b494b8cb7cc5d31ebd4af75b08819139</STR>
    <MAP isArray="true" name="dash" />
    <MAP isArray="true" name="hds" />
    <MAP isArray="true" name="hls" />
    <MAP isArray="true" name="metalistener" />
    <MAP isArray="true" name="mss" />
    <MAP isArray="true" name="process" />
    <MAP isArray="true" name="pull">
    <MAP isArray="true" name="push" />
    <MAP isArray="true" name="record" />
    <MAP isArray="false" name="serverVersion">
        <STR name="banner">EvoStream Media Server (www.evostream.com) version 2.0.0 build 5477 with hash: 373144c364458a5c0a212237a62bcf7ee5af2dfb on branch: release/2.0.0/main - QBert - (built for Microsoft Windows 10 Pro-10.0.14393-x86_64 on 2017-08-04T10:18:20.000)</STR>
        <STR name="branchName">release/2.0.0/main</STR>
        <STR name="buildDate">2017-08-04T10:18:20.000</STR>
        <STR name="buildNumber">5477</STR>
        <STR name="codeName">QBert</STR>
        <STR name="hash">373144c364458a5c0a212237a62bcf7ee5af2dfb</STR>
        <STR name="releaseNumber">2.0.0</STR>
    </MAP>
    <UINT32 name="version">26</UINT32>
    <MAP isArray="true" name="webrtc" />
</MAP>
```

------

##Notes:

- 本ファイルを編集しないでください
- サーバーを以前のストリーム情報等なしにクリーンに起動したい場合は、EMSを起動する前に本ファイルを削除してください。
