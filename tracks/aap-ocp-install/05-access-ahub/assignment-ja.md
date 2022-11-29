---
slug: access-ahub
id: ekswy2qc5v6t
type: challenge
title: Automation Hub ダッシュボードへのアクセス
タブ:
- title: Web コンソール
  type: website
  hostname: crc
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: ターミナル 1
  type: terminal
  hostname: crc
難易度: 基本
制限時間: 300
---
この課題では、新しくインストールされた Automation Hub 環境にアクセスします。

## Automation Hub へのアクセス

Automation Hub ダッシュボードにアクセスするには、`admin` ユーザーのパスワードを取得します。

`admin` ユーザーのパスワードにアクセスするには、`Workloads` ドロップダウンで `Secrets` を選択します。

* `Secrets` 内で、`my-automation-hub-admin-password` というラベルのシークレットを選択します。

* `Secret details` ページ内で、パスワードをクリップボードにコピーして、自動コントローラーのサインインページに貼り付けます。

![Secrets](../assets/ahub-copy-password.png)

* Automation Hub ダッシュボードの URL を取得するには、`Networking` ドロップダウンで `Routes` を選択します。

* `Routes` 内のプロジェクト `ansible-automation-platform` の下で、`https://my-automation-hub-ansible-automation-platform....` で始まる場所が、`my-automation-hub-web-svc` というラベルの付いたサービスに提供されます。

![OCP Routes](../assets/ahub-route.png)

> **_注意:_** URL をクリックすると、Automation Hub のサインインページに移動します。

* ユーザー `admin` とクリップボードにコピーしたパスワードを使用して、Automation Hub ダッシュボードにログインします。

![AHub Dashboard](../assets/ahub_dashboard.png)

お疲れさまでした。以下が正常に行われました。

* Automation Hub のインストール
* Automation Hub ダッシュボードへのアクセス
