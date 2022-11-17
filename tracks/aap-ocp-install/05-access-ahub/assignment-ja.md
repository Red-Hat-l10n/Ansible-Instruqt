---
slug: access-ahub
id: ekswy2qc5v6t
type: challenge
title: Automation Hub ダッシュボードへのアクセス
タブ:
- Web コンソール
  type: website
  hostname: crc
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: ターミナル 1
  type: terminal
  hostname: crc
難易度: 基本
-T timelimit
---
このチャレンジでは、新たにインストールした Automation Hub 環境にアクセスします。

## Automation Hub へのアクセス

Automation Hub ダッシュボードにアクセスするには、`admin` ユーザーのパスワードを取得します。

`admin` ユーザーのパスワードにアクセスするには、`Workloads` ドロップダウンメニューで `Secrets` を選択します。

* `Secrets` 内で、`my-automation-hub-admin-password` というラベルが付けられたシークレットを選択します。

* `Secret details` ページ内でパスワードをクリップボードにコピーして、Automation Controller のサインインページに貼り付けます。

シークレット

* Automation Hub ダッシュボードの URL を取得するには、`Networking` ドロップダウン内の `Routes` を選択します。

* `Routes` 内のプロジェクトの `ansible-automation-platform` で、`https://my-automation-hub-ansible-automation-platform...` で始まる場所が `my-automation-hub-web-svc` というラベルの付いたサービスについて指定されます。

![OCP ルート](../assets/ahub-route.png)

> **_注記：_** URL の場所は、Automation Hub のサインインページに移動します。

* ユーザー `admin` と、クリップボードにコピーされたパスワードを使用して Automation Hub ダッシュボードにログインします。

![AHub ダッシュボード](../assets/ahub_dashboard.png)

お疲れさまでした。以下が正常に行われました。

* Automation Hub がインストールされていること
* Automation Hub ダッシュボードにアクセスします。
