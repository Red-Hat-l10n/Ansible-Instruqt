---
slug: backupjob
id: i1o2ap0i8b2l
type: challenge
title: ネットワークバックアップ自動ジョブの実行
teaser: ラボ 1、課題 2、自動コントローラーでジョブを実行する方法を学ぶ
注記:
- type: text
  コンテンツ: |+
    # 課題 2: バックアップ自動化ジョブの実行

    この課題は、1 回目の課題で作成したバックアップジョブを実行するために、Automation controller を使用する手順を説明します。

    プロビジョニングを開始していない場合は、右下隅にある緑色の開始ボタン <img src="https://github.com/IPvSean/pictures_for_github/blob/master/start_button.png?raw=true" width="100px" align="left"> をクリックします。

- type: text
  コンテンツ: |+
    # Ansible Collections

    Ansible は、自動化コンテンツをコレクションという形で提供します。 Ansible Collection には、ネットワークエンジニアが自動化を構築し、カスタマイズするために使用するモジュール、プラグイン、ロールが含まれています。

    Ansible Collection の簡単な初心者向け情報が必要な場合は、[こちらの YouTube ビデオ](https://www.youtube.com/watch?v=WOcqhk7TdYc&t=69s) を参照してください。

    <center><iframe width="560" height="315" src="https://www.youtube.com/embed/WOcqhk7TdYc" title="YouTube ビデオプレーヤー" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

- type: text
  contents: |
    # Cisco IOS コレクション

    このデモでは、Cisco IOS-XE ルーターに対して自動化する予定です。 Cisco IOS コレクションを使用する必要があります。

    モジュールを使用するための FQCN (または完全修飾コレクション名) です。

    `namespace.collection.module`

    この例では、以下のようになります

    `cisco.ios.<module name>`

    このタスクは、以下のようになります。

    ```
    - name: backup cisco ios configuration
      cisco.ios.config:
        backup: true
      register: config_output
     ```
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
- title: Visual Studio コード
  type: service
  hostname: controller
  path: /editor/
  port: 443
難易度: 基本
制限時間: 600
---
この演習では、Automation controller で自動化ジョブを実行します

# ステップ 1: Automation controller へのログイン
Automation controller にログインするには、画面上部にある `Automation controller WebUI` タブを選択します。

以下の認証情報でログインしてください。

ユーザー名: `admin`<br>
パスワード: `ansible123!`

# ステップ 2 - ネットワーク自動化の実行 - バックアップジョブテンプレート

- 左のナビゲーションメニューのリソースの下にある **テンプレート** をクリックして、**ジョブテンプレート** に移動します。<img src="https://github.com/IPvSean/pictures_for_github/blob/master/job_templates.png?raw=true" width="150px">
- **ネットワークの自動化 - バックアップジョブテンプレート** を実行するには、Launch Job ボタンをクリックし、rocket ボタンをクリックします。

<img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true">

# ステップ 3: オプション：バックアップの確認

Visual Studio Code タブで、バックアップの設定を開くことができます。 Visual Studio Code で `/backup` ディレクトリーを開き、最新のタイムスタンプに移動します。 複数回実行した場合は、複数のオプションがあります。 `cisco.txt` ファイルを開き、Cisco IOS-XE の実行設定を表示します。

# ステップ 4: 検証

下の緑の `Check` ボタンをクリックして、ジョブが実行されたことを確認します。


