---
slug: install-aap-operator
id: sxbtlgndp8nj
type: challenge
title: AAP Operator のインストール
注記:
- type: text
  コンテンツ: |-
    # ようこそ

    Ansible Automation Platform (AAP) を OpenShift にインストールする方法を学ぶ準備をしましょう。

    次の課題では、いかに簡単に数分で実行することが可能かを紹介し、OpenShift 環境で AAP を使用できるようにします。

    使用可能になったら、残りの時間で新しい Ansible Automation Platform 2 を試してみてください。また、https://www.ansible.com/products/ansible-training にある他のラボもすべてチェックしてください。
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
制限時間: 600
---
この課題では、OpenShift クラスターダッシュボードにログインし、Ansible Automation Platform Operator をインストールします。

Ansible Automation Platform Operator をインストールすると、Red Hat OpenShift 上に Ansible Automation Platform コンポーネントをデプロイおよび管理することができるようになります。

## ダッシュボード経由でクラスターにログインする

Web コンソールにログインするには、画面の上部にある *Web Console* タブをクリックします。

次の認証情報を使用して、`admin` ユーザーとしてログインできます。

* ユーザー名:
```
admin
```
* パスワード:
```
admin
```
![Web Console Login](https://raw.githubusercontent.com/openshift-instruqt/instruqt/master/assets/middleware/pipelines/web-console-login.png)

ダッシュボードにログインしたら、`Operators -> OperatorHub` を選択します。

OperatorHub 検索バー内で `ansible` と入力して、Ansible Automation Platform Operator を検索してください。

![OperatorHub](../assets/OperatorHub_access.png)

Ansible Automation Platform Operator を選択し、`Install` を選択します。
![AAP_Install](../assets/select_aap_operator_1.png)

`Install Operator` ウィンドウ内で、`Update channel` 内の `stable-2.2-cluster-scoped` ラジオボタンが選択され、`Installation mode` が `All namespaces on the cluster (default)` 設定されていることを確認します。

> **_注記:_** デフォルトでは、名前空間 `ansible-automation-platform` が存在しない場合は作成されますが、必要に応じて別の名前空間を作成または使用できます。最後に、`Update approval` で `Automatic` を選択し、`Install` をクリックします。

![Install Operator](../assets/operator_install_1.png)

> **_注記:_** Ansible Automation Platform Operator のインストールが完了するまでに数分かかります。

`Installed operator - ready for use` が表示されたら、`View Operator` ボタンを選択します。

お疲れさまでした。これで、Ansible Automation Platform Operator のインストールが完了しました。

次の課題では、Operator からのコンポーネントの 1 つ、具体的には `Automation Controller` のデプロイに焦点を当てます。

> **_警告:_** 次のチャレンジにアクセスする前に、Ansible Automation Platform Operator によってデプロイされた Pod が稼働している必要があります。稼働していない場合は、チェックに失敗します。
