---
slug: servicenow-inventory
id: vyoxhzmu9zr5
type: challenge
title: ServiceNow をインベントリーソースとして使用
teaser: CMDB に対する高度なクエリーの実行と結果への対応
注記:
- type: text
  コンテンツ: |-
    **ご存知ですか?**
    Ansible はエージェントレスであり、ターゲットマシンで実行されている SSH サービスのみ必要です。ただし、これらの課題では、Ansible が ServiceNow などの外部サービスと対話できるようにする API がターゲットです。
タブ:
- title: VS Code
  type: service
  hostname: controller
  path: /editor/?folder=vscode-remote%3A%2F%2F%2fhome%2Frhel%2Fservicenow_project
  port: 443
- title: Automation Controller
  type: service
  hostname: controller
  port: 443
- title: ServiceNow
  type: website
  hostname: controller
  url: https://ansible.service-now.com
  new_window: true
難易度: 基本
timelimit: 400
---
👋 はじめに
====
ここまで、自動化されたインシデント管理プロセスの一部として利用できる `servicenow.itsm` のモジュールいくつか見てきました。モジュールの詳細を確認する中で実行した対話は、実稼働環境に実装する方法とはおそらく異なりますが、このコレクションに含まれるモジュールは非常に柔軟で、ITSM 内のさまざまなユースケースに適用できます。

ITSM タスクとは別に、`servicenow.itsm` コレクションには、CMDB からエンドポイントをクエリーできる非常に便利なインベントリースクリプトもあります。

Automation Controller に新しいインベントリーが追加されましたが、まだどのホストに対してもクエリーは実行していません。詳しく見てみましょう。

👀 インベントリーのレビュー
====
- まず、Automation Controller タブを開き、右側のナビゲーションペインで `Hosts` に移動します。このリストが空であることに注意してください。これは、Ansible Automation Platform と ServiceNow の統合がAPI 間の統合であり、ターゲットとなるエンドポイントがホストではなく API であるためです。

▶️ ServiceNow インベントリーの統合
====
- 次に、左側のナビゲーションペインを使用して `Inventories` を選択します。ここでは `ServiceNow inventory` が新しくなっています。これをクリックしてください。次に `Sources` タブと `Sync` 🔄 ボタンを選択します。

一連のジョブが開始され、ServiceNow CMDB からプルするインベントリーが更新されます。
- 左側のナビゲーションペインから `Jobs` を選択すると、更新の進捗を監視できます。

🔍 検証結果
====
- 2 つのジョブが完了したら、左側のナビゲーションで `Hosts` をクリックし、CMDB からプルされたすべてのホストを確認します。
- また、Inventories > ServiceNow inventory > Hosts でホストとグループも確認します。

このインベントリーは、さまざまな方法で分割できます。このインベントリーに提供されるインベントリークエリーは以下のとおりです。
```
# Group hosts automatically, according to values of manufacturer and os columns.
# Include only records with the specified operating systems.
# Groups will most likely overlap.
plugin: servicenow.itsm.now
group_by:
  manufacturer:
  os:
    includes:
      - Linux Red Hat
      - Windows XP
```
> 上記のインベントリーは、CMDB for Linux および Windows XP オペレーティングシステムをクエリーし、製造元ごとに結果をグループ化しています。

🎉 すべて完了 🎉

NORMAL で問題が発生していますか ?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] してください (https://github.com/ansible/instruqt/issues/new?labels=getting-started-servicenow-automation&title=New+servicenow+issue:+servicenow-inventory&assignees=cloin)。