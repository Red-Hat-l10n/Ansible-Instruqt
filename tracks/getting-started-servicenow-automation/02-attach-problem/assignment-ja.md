---
slug: attach-problem
id: uk5rmgfihy3s
type: challenge
title: 問題の割り当て
teaser: 既存のインシデント番号のクエリーと問題を参照するインシデントの割り当て
注記:
- type: text
  コンテンツ: |-
    **ご存知ですか?**
    Ansible は YAML で記述されています。YAML は簡単に習得できるテキスト形式で、YAML ファイルを読むだけで自動化タスクが作成された目的をすぐに理解できます。
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
ServiceNow の問題は、1 つ以上のインシデントが原因で発生します。作成時には問題の根本原因が判明しない場合もあり、問題管理プロセスの中で根本原因の分析が必要になる可能性があります。

VS Code の作業ディレクトリーに別の Playbook が追加され、先に作成したインシデントに問題を割り当てるためのテンプレートが作成されました。

- まず、`VS Code` タブで `problem-attach.yml` という名前の Playbook を検証します。

> この Playbook は、まず作成した既存インシデントの番号をクエリーし、問題を作成するタスクで返された値を使用することに注意してください。

▶️ 問題の割り当て
====
- 次に、`Resources > Templates` に移動し、テンプレート `2 - Attach problem (problem-attach.yml)` の横にあるロケットアイコンを押して、Automation Controller から新しいジョブテンプレートを実行します。

🔍 検証結果
====
これで正常に完了しているはずです。ServiceNow に戻り、割り当てられた問題で新しい問題番号を確認します。

![new problem](../assets/new-problem.png)

`Self-service - Incidents` でインシデント番号を選択し、インシデントのステータスが更新されたか確認することもできます。また、インシデントページでも問題が参照されているはずです。

以下の緑色の Next ボタンを選択して、次のセクションに移動します。

🐛 問題が発生しましたか?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] してください (https://github.com/ansible/instruqt/issues/new?labels=getting-started-servicenow-automation&title=New+servicenow+issue:+attach-problem&assignees=cloin)。