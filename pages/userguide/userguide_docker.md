---
title: Using EMS on Docker
keyword: docker
sidebar: userguide_sidebar
permalink: userguide_docker.html
folder: userguide
toc: false
---

**Docker**は開発者やシステム管理者が、ラップトップやデータセンターや、VMやクラウド上でアプリケーションをビルド・実行できるオープンなプラットフォームです。- Docker [website](https://www.docker.com/)


Ubuntu 16.04のEMS 2.0.0用のDockerイメージをビルド・実行する方法についての簡易的な説明です。
Dockerそのものについての説明はありません。Dockerについて詳しくは[official Docker documentation](https://docs.docker.com/)をご覧ください。



## Docker上でのEMSの実行

**事前準備:**

- Dockerをインストールしてください

**手順:**

1. EMS dockerイメージを**プル**する:

   ```
   sudo docker pull evostream/<EMS version>-<OS>:<build number>

   例:
   sudo docker pull evostream/ems201-ubuntu1604:5649
   ```

   **利用可能なイメージ:**

   - evostream/ems200-ubuntu1604:5550


   - evostream/ems201-ubuntu1604:5649

   **Note:** [Docker store](https://store.docker.com)で利用可能なイメージを確認できます

   ​

2. コンソールからDockerを管理者モードで**実行**します

   ```
   $ sudo su
   # dockerd &
   # exit
   ```

   **Notes:**

   - Dockerはdaemonとして実行されます
   - rootになるとプロンプトは`#`が表示され、通常ユーザーモードでは`$`が表示されます。管理者モードで下記のコマンドを実行する場合は`sudo`をつける必要はありません
   - `ps -e|grep docker`でdockerの実行状況を確認できます

   ​

3. Dockerの**テスト**


   Dockerのインストールがうまくいったかどうかを"hello world"デモを実行して確認してください。ここで作成されたimageファイルは後で削除して結構です。

   ```
   $ sudo docker run --name hello hello-world
   $ sudo docker ps -a
   $ sudo docker images
   $ sudo docker rmi hello-world
   ```

4. EMS Docker Imageの**実行**

   Docker HubのEvoStream public repositoryのビルド済みDocker image for EMSを使えるよう下記のスクリプトを実行してください。


   ```
   sudo docker run --name <container_name> -i -t -p \
     -p 1112:1112/tcp \
     -p 1222:1222/tcp \
     -p 1935:1935/tcp \
     -p 4000:4000/tcp \
     -p 4100:4100/tcp \
     -p 5544:5544/tcp \
     -p 6666:6666/tcp \
     -p 7777:7777/tcp \
     -p 8080:8080/tcp \
     -p 8100:8100/tcp \
     -p 8210:8210/tcp \
     -p 8410:8410/tcp \
     -p 8433:8433/tcp \
     -p 8888:8888/tcp \
     -p 9898:9898/UDP \
     -p 9998:9998/tcp \
     -p 9999:9999/tcp \
     <image_name> bash
   ```

5. containerに**ログイン**してください

   コンテナに自動的にログインしない場合は下記のコマンドを使用してください:


   ```
   sudo docker exec -i -t <container_id> /bin/bash

   例:
   sudo docker exec -i -t 3cb068bca5b6 /bin/bash
   ```

   **Note:**  ログインが成功するとプロンプトは`root@<instance_id>` になります

   ​

6. EMSの**起動**

   Docker imageにはEMSライセンスは入っておりません。[EvoStream website](http://evostream.com/)から試用ライセンスを取得するか、
   ホストマシンの`License.lic`ファイルをコンテナ上の`/etc/evostreamms` フォルダまたは `/config`フォルダにコピーしてください。

   ```
   $ sudo docker cp /path/to/License.lic <container_name>:/etc/evostreamms

   例:
   $ sudo docker cp /path/to/License.lic evostream/ems201-ubuntu1604:5649:/etc/evostreamms
   ```

   `sudo docker ps -a`コマンドを使ってコンテナ名を確認してください

   Docker コンテナ内のEMSを管理者権限で起動してください

   ```
   # service evostreamms start
   ```
