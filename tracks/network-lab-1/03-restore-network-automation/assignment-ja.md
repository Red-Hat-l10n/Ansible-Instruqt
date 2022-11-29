---
slug: restore-network-automation
id: 6bm7wqtewfrt
type: challenge
title: ネットワーク復元自動ジョブの実行
teaser: ラボ 1、課題 3、ネットワークリストアジョブの実行
注記:
- type: text
  コンテンツ: |+
    # 課題 3: 復元自動化ジョブの実行

    この課題は、1 回目の課題で作成した復元ジョブを実行するために、Automation controller を使用する手順を説明します。

    プロビジョニングを開始していない場合は、右下隅にある緑色の開始ボタン <img src="https://github.com/IPvSean/pictures_for_github/blob/master/start_button.png?raw=true" width="100px" align="left"> をクリックします。

- type: text
  コンテンツ: |-
    # 仕組み

    1. ネットワークオペレータは、前回のチャレンジで行ったように、`ネットワークの自動化 - バックアップ` ジョブを実行します
    2. 自動化ジョブは、Cisco IOS ルーターから設定を取得します。
    3. 自動化ジョブは、指定された `バックアップサーバー` にそれを保存します
    4. ネットワークオペレーターの最後に、自動化ジョブは `ネットワークの自動化 - ジョブテンプレート` を自動的に作成し、Survey を介して選択できるように、ネットワークオペレーターで利用可能なすべてのバックアップを追加します

    実際には、`ansible.controller` Ansible Collection を使用して、簡単なタスクでAutomation controller を自動化できます。
- type: text
  コンテンツ: |-
    # 仕組み: アニメーション


    <center>
    <img src="https://github.com/IPvSean/pictures_for_github/blob/master/network-backup.gif?raw=true"></center>
- type: text
  コンテンツ: |-
    # Survey

    Survey は、Prompt for Extra Variables （追加変数のプロンプト）と同様に Playbook の追加変数を設定しますが、ユーザーフレンドリーな質問と回答を使ってこれを実行します。Survey では、ユーザー入力を検証することもできます。
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
この演習では、ネットワークリストアの自動化ジョブを実行します

# ステップ 1: Automation controller へのログイン
Automation controller にログインするには、画面上部にある `Automation controller WebUI` タブを選択します。

以下の認証情報でログインしてください。

ユーザー名: `admin`<br>
パスワード: `ansible123!`

# ステップ 2 - ネットワーク自動化の実行 - ジョブテンプレートの復元

- 左のナビゲーションメニューのリソースの下にある **テンプレート** をクリックして、**ジョブテンプレート** に移動します。<img src="https://github.com/IPvSean/pictures_for_github/blob/master/job_templates.png?raw=true" width="150px">
- **ネットワークの自動化 - バックアップジョブテンプレート** を実行するには、Launch Job ボタンをクリックし、rocket ボタンをクリックします。

<img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true">

# ステップ 3: 検証

下の緑の `Check` ボタンをクリックして、ジョブが実行されたことを確認します。


