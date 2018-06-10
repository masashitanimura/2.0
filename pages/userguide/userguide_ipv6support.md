---
title: Using IPv6
keywords: demo
sidebar: userguide_sidebar
permalink: userguide_ipv6support.html
folder: userguide
toc: false
---

EMSはIPv6をサポートしています

config.luaおよびwebconfig.luaでIPアドレスバインドをv6 IPアドレスフォーマットに変更し、EMSを再起動してください。

*変更例:*

```
-- RTMP and clustering
				{
					ip="::",
					port=1935,
					protocol="inboundRtmp",
				},
				{
					ip="::",
					port=1936,
					protocol="inboundRtmp",
					clustering=true
				},
				{
					ip="::",
					port=1113,
					protocol="inboundBinVariant",
					clustering=true
				},
```

**Notes:**

- **127.0.0.1** を **::**に変更してください
- URLにipv6を使う場合は **[ipv6:port]**と記述してください
- EMSは"**localhost**"を"**127.0.0.1**"と名前解決します
- EMSサービスがv6アドレスにバインドされいている場合はコマンドもv6を使用してください
- `pullStream`コマンドをv6アドレスで実行する際は、サービスがv6アドレスにバインドされていることを確認してください
