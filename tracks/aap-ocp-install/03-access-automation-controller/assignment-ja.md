---
slug: access-automation-controller
id: nudioocrzqv2
type: challenge
title: 自動コントローラーのダッシュボードへのアクセス
タブ:
- title: Web コンソール
  type: website
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: ターミナル 1
  type: terminal
  hostname: crc
- title: Ansible
  type: terminal
  hostname: ansible
難易度: 基本
制限時間: 600
---
この課題では、新しくインストールされた自動コントローラー環境にアクセスします。

## 自動コントローラーへのアクセス

自動コントローラーのダッシュボードにアクセスするには、`admin` ユーザーのパスワードを取得します。

`admin` ユーザーのパスワードにアクセスするには、`Workloads` ドロップダウンで `Secrets` を選択します。

* `Secrets` 内で、`my-automation-controller-admin-password` というラベルのシークレットを選択します。

* `Secret details` ページ内で、パスワードをクリップボードにコピーして、自動コントローラーのサインインページに貼り付けます。

![Secrets](../assets/copy-password.png)

* 自動コントローラーのダッシュボード URL を取得するには、`Networking` ドロップダウンで `Routes` を選択します。

* `Routes` 内のプロジェクト `ansible-automation-platform` の下で、`https://my-automation-controller-ansible-automation-platform....` で始まる場所が、`my-automation-controller-service` というラベルの付いたサービスに提供されます。

![OCP Routes](../assets/my-automation-controller-route.png)

> **_注記:_** URL をクリックすると、自動コントローラーのサインインページに移動します。

自動コントローラーのサインインページがロードされていない場合は、インストールプロセスがまだ進行中であることを意味します。Ansible Automation Platform が完了していないことを示す画面の例を以下に示します。

![AAP In Progress](../assets/aap_in_progress.png)

* ユーザー `admin` とクリップボードにコピーしたパスワードを使用して、自動コントローラーダッシュボードにログインします。

![AAP Dashboard](../assets/aap_dashboard.png)

お疲れさまでした。以下が正常に行われました。

* Operator 経由での Ansible Automation Platform のインストール
* 自動コントローラーのインストール
* 自動コントローラーのダッシュボードへのアクセス
