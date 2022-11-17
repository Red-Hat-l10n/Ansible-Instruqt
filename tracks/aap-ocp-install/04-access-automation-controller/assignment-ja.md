---
slug: access-automation-controller
id: nudioocrzqv2
type: challenge
title: 自動化コントローラーダッシュボードへのアクセス
タブ:
- title: Web コンソール
  type: website
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: ターミナル 1
  type: terminal
  hostname: crc
難易度: 基本
timelimit: 300
---
このチャレンジでは、新たにインストールした自動化コントローラー環境にアクセスします。

## automation controller

自動化コントローラーダッシュボードにアクセスするには、`admin` ユーザーのパスワードを取得します。

`admin` ユーザーのパスワードにアクセスするには、`Workloads` ドロップダウンメニューで `Secrets` を選択します。

* `Secrets` 内で、`my-automation-controller-admin-password` というラベルが付けられたシークレットを選択します。

* `Secret details` ページ内でパスワードをクリップボードにコピーして、Automation Controller のサインインページに貼り付けます。

シークレット

* 自動化コントローラーダッシュボードの URL を取得するには、`Networking` ドロップダウン内の `Routes` を選択します。

* `Routes` 内のプロジェクトの `ansible-automation-platform` で、`https://my-automation-controller-ansible-automation-platform...` で始まる場所が `my-automation-controller-service` というラベルの付いたサービスについて指定されます。

![OCP ルート](../assets/my-automation-controller-route.png)

> **_注記：_** URL の場所は、自動化コントローラーのサインインページに移動します。

自動化コントローラーのサインインページが読み込まれていない場合は、インストールプロセスが進行中であることを意味します。Ansible Automation Platform が完了していないことを示す画面の例を以下に示します。

![AAP 進行中](../assets/aap_in_progress.png)

* ユーザー `admin` と、クリップボードにコピーされたパスワードを使用して自動化コントローラーダッシュボードにログインします。

![AAP ダッシュボード](../assets/aap_dashboard.png)

お疲れさまでした。以下が正常に行われました。

* Operator 経由でインストールした Ansible Automation Platform
* インストールされた自動化コントローラー
* Automation controller ダッシュボードへようこそ。
