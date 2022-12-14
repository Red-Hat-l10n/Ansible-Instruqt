---
slug: edge-playground
id: ndvesxlpe1kf
type: challenge
title: プレイグラウンド
teaser: 残りの時間を使って、新しいスキルを磨いたり、ラボを探索したりしてください。
注記:
- type: text
  コンテンツ: |-
    # 自身のアドベンチャーを選んでください!
    #### いくつかのアイデア:
    #### このプレイグラウンドを使用して、Red Hat Ansible Automation Platform のグローバル設定を確認します
    #### 自動化ワークフローをステップごとに自分で再作成する
    #### このセッションで使用された Playbook を確認してください
    #### アプリケーションまたは monitoring ダッシュボードにログインして探索
タブ:
- title: コントローラー
  type: service
  hostname: controller-edge-lab
  port: 443
- title: Jhb アプリ
  type: service
  hostname: jhb-edge-lab
  path: /web/login
  port: 8088
  new_window: true
- title: Jhb mon
  type: service
  hostname: jhb-edge-lab
  path: /network
  port: 9090
  url: https://jhb-edge-lab:9090
  new_window: true
- title: Dublin アプリケーション
  type: service
  hostname: dublin-edge-lab
  path: /web/login
  port: 8088
  new_window: true
- title: Dublin mon
  type: service
  hostname: dublin-edge-lab
  path: /network
  port: 9090
  url: https://dublin-edge-lab:9090
  new_window: true
難易度: 基本
時間制限: 600
---

🔐 ミッションのログイン認証情報
===

>**コントローラーおよびモニターリングのユーザー名**:
> ```yaml
>student
>```
>**コントローラーおよびモニターリングパスワード**:
>```yaml
>learn_ansible
>```

>**Ignition ユーザー名**:
> ```yaml
>admin
>```
>**Ignition パスワード**:
>```yaml
>learn_ansible
>```

👋 はじめに
===
このセットアップをプレイグラウンドとして自由に使用できます。

##### ⏰ プレイ時間: *10 分*

>**❗️注意**
>
>* 必要な場合は、_Controller_ タブから提供された認証情報を使用して自動化コントローラーにログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。
>* 以下は、この例で使用されている Playbook への [リンク](https://github.com/craig-br/instruqt-track-content/tree/devel/getting-started-edge-lab/playbooks) です。

* ワークフローを再作成する場合は、イメージを参照として確認してください。

<a href="#wf">
  <img alt="Autodeploy workflow" src="../assets/img/wf.png" />
</a>

<a href="#" class="lightbox" id="wf">
  <img alt="Autodeploy workflow" src="../assets/img/wf.png" />
</a>