---
slug: networkreportjob
id: i1o2ap0i8b2l
type: challenge
title: ネットワークレポート自動ジョブの実行
teaser: ラボ 1、課題 2、自動コントローラーでジョブを実行する方法を学ぶ
注記:
- type: text
  contents: |
    # 課題 2 - ネットワークオートメーションの実行 - レポートジョブ

    この課題は、1 回目の課題で作成した `ネットワークの自動化 - レポート` を実行するために、Automation controller を使用する手順を説明します。
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
    - name: retrieve cisco facts
      cisco.ios.facts:
        gather_subset: config
        gather_network_resources: ospf
     ```
- type: text
  コンテンツ: |-
    # ネットワークの自動化は事実に始まり、事実に終わる

    各ネットワークリソースモジュールは、その特定のリソースに関する fact を取得することができます。 例えば、VLAN 情報を取得したい場合、Arista、Cisco、Juniper のネットワークデバイスから YAML または JSON データ構造を返すことができます。

    <img src="https://github.com/IPvSean/pictures_for_github/blob/master/retrieve_facts.png?raw=true">
- type: text
  コンテンツ: |-
    # データ出力は柔軟性があります

    Ansible Automation Platform は、fact を伴うカスタマイズされたネットワークレポートを作成することができます。

    <img src="https://github.com/IPvSean/pictures_for_github/blob/master/create_report.png?raw=true">
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
- title: 動的レポート
  type: service
  hostname: controller
  port: 8088
難易度: 基本
制限時間: 600
---
この演習では、Automation controller で自動化ジョブを実行します

# ステップ 1: Automation controller へのログイン
Automation controller にログインするには、画面上部にある `Automation controller WebUI` タブを選択します。

以下の認証情報でログインしてください。

ユーザー名: `admin`<br>
パスワード: `ansible123!`

# ステップ 2 - ネットワーク自動化の実行 - ネットワークレポートジョブテンプレート

- 左のナビゲーションメニューのリソースの下にある **テンプレート** をクリックして、**ジョブテンプレート** に移動します。<img src="https://github.com/IPvSean/pictures_for_github/blob/master/job_templates.png?raw=true" width="150px">
- **ネットワークの自動化 - レポート** ジョブテンプレートを実行するには、Launch Job ボタンをクリックし、rocket ボタンをクリックします<img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true">



# ステップ 3: Open Network Report

ジョブの実行に成功したら、上部の **Dynamic Report** タブをクリックします。 結果が表示されない場合は、必ずタブを更新してください。

更新するには、<img src="https://github.com/IPvSean/pictures_for_github/blob/master/refresh.png?raw=true"> ボタンをクリックします

# ステップ 4: Dynamic Report をクリック

これは仮想の Cisco IOS ルーターなので、物理的なインターフェイスは 1 つしかありません。 ネットワークリソースの周りをクリックすると、リソースボックスがデプロイメントされ、より詳細な情報が表示されます。

このレポートは、非常にシンプルな Jinja2 テンプレートと jQuery UI アコーディオンツールを併用して作成されています。

# ステップ 5: オプション

**Automation controller Terminal** タブに移動し、cisco デバイスにログインします。

```
sudo -i
ssh cisco
```

何か (選択) を設定し、レポートを再実行します。

例:

```
cisco-ios-csr-1731#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
```

```bash
router ospf 1
  router-id 1.2.3.4
```

# ステップ.6: 検証

下の緑の `Check` ボタンをクリックして、ジョブが実行されたことを確認します。


