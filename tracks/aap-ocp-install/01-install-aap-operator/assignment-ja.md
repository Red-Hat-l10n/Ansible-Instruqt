---
slug: install-aap-operator
id: sxbtlgndp8nj
type: challenge
title: AAP Operator のインストール
注記:
- type: text
  コンテンツ: |-
    # ようこそ !

    Red Hat OpenShift への Ansible Automation Platform (AAP)のインストール方法については、こちらをご参照ください。

    以下の課題では、OpenShift 環境で AAP を簡単に確認し、簡単に稼働させる方法を紹介します。

    これが利用可能になったら、残りの時間で新しい Ansible Automation Platform 2 を調べ、にある他のラボをすべてチェックアウトしてください。 https://www.ansible.com/products/ansible-training
タブ:
- title: ターミナル 1
  type: terminal
  hostname: crc
- title: Web コンソール
  type: website
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: Visual Editor
  type: code
  hostname: crc
  path: /root
難易度: 基本
timelimit: 600
---
このチャレンジでは、OpenShift クラスターダッシュボードにログインし、Ansible Automation Platform Operator をインストールします。

Ansible Automation Platform Operator をインストールすると、Red Hat OpenShift に Ansible Automation Platform コンポーネントをデプロイし、管理できます。

## Dashboard を使用したクラスターへのログイン

Web コンソールにログインするには、画面上部付近の *Web* コンソール タブをクリックします。

以下の認証情報を使用して `admin` ユーザーとしてログインできます。

* ユーザー名:
```
admin
```
* パスワード：
```
admin
```
![Web Console Login](https://raw.githubusercontent.com/openshift-instruqt/instruqt/master/assets/middleware/pipelines/web-console-login.png)

ダッシュボードにログインしたら、`Operators -> OperatorHub` を選択します。

OperatorHub 検索バー内で、`ansible` と入力して Ansible Automation Platform Operator を検索します。

![OperatorHub](../assets/OperatorHub_access.png)

Ansible Automation Platform Operator を選択し、Install `を` 選択します。
![AAP_Install](../assets/select_aap_operator_1.png)

`Install Operator` ウィンドウで、`Update チャネル` 内の `stable-2.2-cluster-scoped` ラジオボタンが選択され、`Installation モード` が `All namespaces on the cluster (default)` に設定されていることを確認します。

> **_注記：_** デフォルトでは、namespace `ansible-automation-platform` が存在しない場合は作成されますが、必要な場合は別の namespace を作成するか、使用することができます。最後に、`Update approval` に `Automatic` を選択し、`Install` をクリックします。

![Install Operator](../assets/operator_install_1.png)

> **_注記：_** Ansible Automation Platform Operator のインストールが完了するまでに数分かかります。

`Installed operator - ready for use` が表示されたら、`View Operator` ボタンを選択します。

お疲れさまでした。これにより、Ansible Automation Platform Operator のインストールが完了しました。

次の課題では、Operator からのコンポーネント（特に `Automation Controller` ）の 1 つをデプロイすることに重点を置いています。

> **_警告：_** 次のチャレンジにアクセスする前に、Ansible Automation Platform Operator によってデプロイされた Pod が稼働している必要があります。そうしないと、チェックに失敗します。
