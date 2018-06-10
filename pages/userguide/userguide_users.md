---
title: users.lua
keywords: authentication
sidebar: userguide_sidebar
permalink: userguide_users.html
folder: userguide
toc: false
---

EMSにストリームがプッシュされる際に必要となる認証情報を定義します

定義箇所:

- user1 = user1のユーザ名
- user2 - user2のユーザ名
- password1 = user1のパスワード
- password2 = user2のパスワード

```
users=
{
	user1="password1",
	user2="password2",
}

realms=
{
	{
		name="EVOSTREAM stream router",
		method="Digest",
		users={
			"user1",
			"user2",
		},
	},
}
```

------

## Notes:

- 本ファイル内のユーザ名の追加・削除を行っていただけます。
- 本ファイルを適用するには認証(auth.xml)が有効になっている必要があります。


------

## 関連リンク

- [auth.xml](userguide_auth.html)
