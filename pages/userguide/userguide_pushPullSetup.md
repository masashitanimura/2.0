---
title: pushPullSetup.xml
keywords: pushPullSetup
sidebar: userguide_sidebar
permalink: userguide_pushPullSetup.html
folder: userguide
toc: false
---



This file is used by the EMS to store stream action commands that are made through the Runtime API. The most important thing to know about the pushPullSetup.xml file is that it **should not be modified manually**!. At startup, if the EMS detects that the file has been modified it will rename the file and start with a blank/fresh copy.

This file is used for internal purposes only. If, during startup, the EMS detects that changes have been made to the pushPullSetup.xml file, it will rename the existing pushPullSetup.xml file and start with a fresh configuration.

Now that the disclaimer is out of the way, it is important to understand how this file is used. When a `pullStream`, `pushStream`, `createHLSStream`, `createHDSStream`, `createMSSStream`, `createDASHStream`, `record`, or `launchProcess`, or `startWebRtc` command is executed, that command is logged to this file (assuming the `keepAlive` flag is **1**, which it is by default). 

When the EMS is started, it parses this file and attempts to recreate all of the connections. These configuration entries can be removed by issuing `removeConfig` commands, or by setting the `keepAlive` flag to **0** when the initial command is made.

**Note:** If you wish to have a “clean start” of the server, with no previous streams, you may delete this file before starting the EMS.

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <STR name="checksum">b494b8cb7cc5d31ebd4af75b08819139</STR>
    <MAP isArray="true" name="dash" />
    <MAP isArray="true" name="hds" />
    <MAP isArray="true" name="hls" />
    <MAP isArray="true" name="mss" />
    <MAP isArray="true" name="process" />
    <MAP isArray="true" name="pull">
    <MAP isArray="true" name="push" />
    <MAP isArray="true" name="record" />
    <MAP isArray="false" name="serverVersion">
        <STR name="banner">EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491 with hash: 64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin/release/1.7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)</STR>
        <STR name="branchName">origin/release/1.7.0.1</STR>
        <STR name="buildDate">2016-06-17T09:33:23.000</STR>
        <STR name="buildNumber">4491</STR>
        <STR name="codeName">PacMan|m|</STR>
        <STR name="hash">64b305253110afc4acd5aeaf87f0a0b0f9b53526</STR>
        <STR name="releaseNumber">1.7.1</STR>
    </MAP>
    <UINT32 name="version">26</UINT32>
    <MAP isArray="true" name="webrtc" />
</MAP>

```

