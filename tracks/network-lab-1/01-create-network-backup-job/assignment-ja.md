---
slug: create-network-backup-job
id: hy7xyooj7xca
type: challenge
title: バックアップ自動ジョブテンプレートの作成
teaser: ラボ 1、課題 1、自動化でバックアップジョブテンプレートを作成する方法を学ぶ
  controller
注記:
- type: text
  contents: |
    # ラボ 1 - 設定のバックアップおよび復元

    このラボでは、Automation controller を使用して、バックアップを自動化し、IOS-XE を実行している Cisco CSR (クラウドサービスルーター) の設定を復元する方法について説明します。

    プロビジョニングを開始していない場合は、右下隅にある緑色の開始ボタン <img src="https://github.com/IPvSean/pictures_for_github/blob/master/start_button.png?raw=true" width="100px" align="left"> をクリックします。
- type: text
  コンテンツ: |-
    # ラボダイアグラム

    このデモのラボ図は非常に簡単です。 Automation controller を実行する Red Hat Enterprise Linux 8 デバイスが 1 つあります。 IOS-XE が動作する Cisco CSR (クラウドサービスルーター) の管理ネットワークに直結しています。

    <center><img src="https://github.com/IPvSean/pictures_for_github/blob/master/lab1-topo.png?raw=true" width="400"></center>
- type: text
  コンテンツ: |-
    # クイックオートメーションビクトリー

    ネットワークのバックアップとリストアは、全体から見ればあまり面白いものではありません。すべてのネットワークオペレーターが必要とする、非常に一般的でユビキタスなユースケースであることは分かっています。これにより、ネットワークエンジニアが自動化の道を歩み始めるための、簡単なターンキーユースケースを提供します。
- type: text
  コンテンツ: |-
    # Automation controller

    Automation controller は、企業全体で Ansible 自動化を定義、運用、委任するための標準化された方法を提供します。この課題では、WebUI (Web User Interface) を使用します。
- type: text
  コンテンツ: |-
    # ジョブテンプレート

    オートメーションコントローラーのすべては、**ジョブテンプレート** の概念を中心に展開されています。 ジョブテンプレートは、Ansible Playbook を組織で制御、委譲、拡張することを可能にします。

    また、ジョブテンプレートは、Ansible Playbook コンテンツの再利用とチーム間のコラボレーションを促進します。

    ジョブテンプレートには以下が必要です。
    - ジョブを実行するための **インベントリー**
    - デバイスにログインするための **認証情報**。
    - Ansible Playbook を含む **プロジェクト**
- type: text
  コンテンツ: |-
    # 課題 1: バックアップジョブテンプレートの作成

    この課題演習では、Automation controller でジョブテンプレートを作成します。 今回は、マルチベンダーの Playbook を含む Network Toolkit Collection (https://github.com/network-automation/toolkit) を使用して、バックアップ、復元などを行います。

    **認証情報** (ユーザー名とパスワード)、**インベントリー** (Cisco ルーター 1 台)、**プロジェクト** (上記のネットワークツールキットリポジトリー) はすでに追加されています。 組織で使用できるように、簡単に再利用可能なジョブテンプレートに関連付ける必要があります。
- type: text
  コンテンツ: |-
    # 使ってみる

    これでラボの概要の終了です。

    ラボのセットアップが完了したら、このウィンドウの右下隅にある緑のスタートボタン (<img src="https://github.com/IPvSean/pictures_for_github/blob/master/start_button.png?raw=true" width="100px" align="left">) をクリックすることができます。
タブ:
- title: 自動コントロラー WebUI
  type: service
  hostname: controller
  port: 443
- title: 自動コントローラーターミナル
  type: terminal
  hostname: controller
難易度: 基本
制限時間: 300
---
この演習では、Automation controller で自動化ジョブを作成します

# ステップ 1: Automation controller へのログイン
Automation controller にログインするには、画面上部にある `Automation controller WebUI` タブを選択します。

以下の認証情報でログインしてください。

ユーザー名: `admin`<br>
パスワード: `ansible123!`

# ステップ 2: 自動化ジョブの作成

- 左のナビゲーションメニューのリソースの下にある **テンプレート** をクリックして、**ジョブテンプレート** に移動します。<img src="https://github.com/IPvSean/pictures_for_github/blob/master/job_templates.png?raw=true" width="150px">
- **ジョブテンプレートの一覧が表示されます**。 ジョブテンプレートは、Ansible プレイブックのコンテンツの再利用やチーム間のコラボレーションを促進します。
- 青い追加ボタンをクリックし、**ジョブテンプレートの追加** を選択します
- 次の値を割り当てます

<table>
  <tr>
    <th>名前</th>
    <th>値</th>
  </tr>
  <tr>
    <td>名前</td>
    <td><code>Network Automation - Backup</code></td>
  </tr>
  <tr>
    <td>ジョブタイプ</td>
    <td><code>Run</code></td>
  </tr>
  <tr>
    <td>インベントリー</td>
    <td><code>Network Inventory</code></td>
  </tr>
  <tr>
    <td>プロジェクト</td>
    <td><code>Network Toolkit</code></td>
  </tr>
  <tr>
    <td>実行環境</td>
    <td><code>Default execution environment</code></td>
  </tr>
  <tr>
    <td>Playbook</td>
    <td><code>playbooks/network_backup.yml</code></td>
  </tr>
  <tr>
    <td>認証情報<br><b>注記:</b> 認証情報は 2 つあります</td>
    <td><ul><li><code>Network Credential</code><li><code>AAP controller credential</code></li></ul></td>
  </tr>
</table>

`AAP コントローラーのクレデンシャルを` 見つけるには、**選択したカテゴリー** を `Red Hat Ansible Automation Platform` に変更します

- 青い **Save** ボタンをクリックして、ジョブテンプレートを保存します。

# ステップ 3: 検証

下の緑の `Check` ボタンをクリックして、ジョブテンプレートが作成されたことを確認します。


