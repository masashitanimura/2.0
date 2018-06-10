---
title: Sending Streams
keyword: pushstream
sidebar: userguide_sidebar
permalink: userguide_send.html
folder: userguide
toc: true
---



## Facebook Live

ローカルストリームをport80を使用してFaceBook liveにプッシュする手順は以下のとおりです：




1. Facebookアカウントに**Log in**します

2. Facebookにプッシュするストリームを選択してください。アクティブなストリームがリスト表示されます

   ![](images/userguide/FB_choosestream.JPG)

3. プッシュしたいストリームの**description** を入力してください

   ![](images/userguide/FB_adddescription.JPG)

4. ライブストリームをどこに**publish**（公開）するかを選択してください。選択肢は:

   - ユーザーのタイムライン: ユーザーのタイムラインにストリームを公開する

   - ページ: 選択したページにストリームを公開する

   - イベント: 選択イベントにストリームを公開する

   - グループ: 選択グループにストリームを公開する

     **Notes**:

     - 複数のページやイベント、グループから選択が可能です
     - 選択できるのはひとつのページ、イベント、グループです
     - 管理しているページやイベント、グループにのみ公開ができます

     ​

   ![](images/userguide/FB_publish.jpg)

   ​

5. **プライバシー設定**

   ![](images/userguide/FB_privacy.JPG)

   Facebookのプライバシー設定を参照 [here](https://www.facebook.com/help/325807937506242/).

   ​

6. **Post to Facebook**ボタンをクリックして公開してください

   ![](images/userguide/FB_sendstream.JPG)


   ​

7. プッシュされたストリームを確認します

   ![](images/userguide/FB_live.JPG)



## YouTube Live

イベントを利用してローカルストリームをYouTubeライブにプッシュする手順は以下です:

**Note:** プッシュされるストリームはRTMPのみ使用可能です

**事前準備:**

- YouTubeアカウントでLiveストリーミングを有効にしてください

  ​

1. Google+アカウントに**ログイン**してください

2. YouTubeにプッシュする**ストリームを選択**してください。アクティブなストリームがリスト表示されます。

   ![](images/userguide/FB_choosestream.JPG)

3. プッシュしたいストリームの**Titleおよびdescription** を入力してください

   ![](images/userguide/G+_titledesc.JPG)

4. ストリームの**プライバシー設定を選択**してください

   - **Public** - ビデオおよびプレイリストをだれでも閲覧できます
   - **Private ** - ビデオおよびプレイリストをあなたおよび選択したユーザのみ閲覧できます
   - **Unlisted** -  ビデオおよびプレイリストをリンクを知っていればだれでも閲覧できます


   ![](images/userguide/FB_privacy.JPG)

   YouTubeのプライバシー設定について [here](https://support.google.com/youtube/answer/157177?co=GENIE.Platform%3DDesktop&hl=en).

   ​

5. ストリームの**フォーマットを選択**してください

   ![](images/userguide/G+_vidformat.JPG)

   **Note:** ビデオフォーマットはストリームフォーマットと同一または低位の設定にする必要があります

   ​

6. **Send Stream to YouTube**ボタンをクリックしストリームを公開します

   ![](images/userguide/G+_sendstream.JPG)


   ​

7. プッシュされたストリームを確認します



## Notes:

- ProfileページでFacebookおよびGoogle+アカウントをアンリンクできます
- UI上でアカウントをアンリンクしても、Facebookアカウント内のEMS Web UIエントリは削除されません、Facebook設定で修正してください
