---
title: Adding Streams
sidebar: userguide_sidebar
permalink: userguide_add.html
folder: userguide
toc: true
---

EMSにストリームを追加することができます。シンプルなストリームやHTTPストリームの追加ができます



## インバウンドライブストリームの追加

`pullStream`コマンドに似ています。RTSPまたはRTMPストリームを追加は次の手順です:

1. **Inbound Live Stream**をプルダウンから選択してください

2.  **URI Stream Source**を入力してください

3. **Local Stream Name**を入力してください

4. **Add Stream**ボタンをクリックしてください

   ![](images/userguide/addstream.JPG)

   ​

**Notes:**

- ![](images/userguide/clear.JPG)  - フィールドの内容を消去します

- ![](images/userguide/viewstream.JPG)   - アクティブなストリームの表示にリダイレクトされます

より詳しい情報は [pullStream](api_pullStream.html) APIをご参照ください



## HTTPストリームの追加

簡単にHTTPストリームの追加ができます。HLS, DASH, HDS, MSSを生成することができます。
A

1. **HTTP Stream Type** （ストリームタイプ）を選択してください(HLS, DASH, HDS, MSS)

2.  **Stream Source**を選択してください

   **Note:** Stream Sourceフィールドにアクティブなストリームがリスト表示されます （複数選択可）

3.  **Target Folder**を入力してください

   **Note:** 絶対パスを入力してください

4. **Group Name**を入力してください

5. **Chunk Length**を入力してください

6. **Bitrate** (オプショナル)を入力してください

7. **Add Stream**をクリックしてください

![](images/userguide/addhttpstream.JPG)



**Notes:**

- ![](images/userguide/clear.JPG)   - フィールドを消去します
- ![](images/userguide/viewstream.JPG)   - アクティブなストリームの表示にリダイレクトされます
