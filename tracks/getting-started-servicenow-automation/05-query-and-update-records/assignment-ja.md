---
slug: query-and-update-records
id: wsjpclhp57g6
type: challenge
title: レコードのクエリーと更新
teaser: 複数タイプの複数レコードのクエリーと更新
注記:
- type: text
  コンテンツ: |-
    **ご存知ですか?**
    Ansible コンテンツは読みやすく、プレーンテキストを使用しているため、Ansible を使用することでコードとしてのインフラストラクチャーを簡単に実現できます。
タブ:
- title: VS Code
  type: service
  hostname: controller
  path: /editor/?folder=vscode-remote%3A%2F%2F%2fhome%2Frhel%2Fservicenow_project
  port: 443
- title: Automation controller
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
ここでは、この学習トラックの一環として作成されたレコードをクリーンアップします。そのために、異なるモジュールを使用して ServiceNow ユーザーが作成したレコードを見つけます。

これを実行するには、VS Code の `close-records-by-user.yml` Playbook を検証します。ここには、新しいモジュールがいくつかあります。これらの `*_info` モジュールは、ユーザー名で作成されたアクティブなレコードのさまざまなレコードタイプ (incident、problem、change_request) のクエリーに使用されています。その後、Ansible はこれらの返されたレコードを単純なオブジェクトリストに変換し、それぞれのモジュールに渡してレコードを更新/クローズします。モジュール自体によって実装されていないフィールドについては、特定のテーブルの他のフィールドまたはカスタムフィールドを指定するために使用できる `other` というモジュールパラメーターがあります。

▶️ レコードのクエリーとクローズ
====
この自動化を実行するには、以下を行います。
- `Resources > Templates` に移動し、automation controller のジョブテンプレート `5 - Query and close records by user (close-records-by-user.yml` を起動します
- ジョブテンプレートの出力を監視し、ジョブが完了するまで待ちます

🔍 検証結果
====
ジョブが完了したら、以前の課題で作成したすべてのレコードをクローズまたは削除する必要があります。ジョブ出力には、クリーンアップされた関連するレコード番号がすべて表示されます。ServiceNow でビューを更新し、更新を確認します。

これですべてクリーンアップされました。次の課題に進んでください。下にある緑色の Next ボタンをクリックします。

🐛 問題が発生しましたか?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成](https://github.com/ansible/instruqt/issues/new?labels=getting-started-servicenow-automation&title=New+servicenow+issue:+query-and-update-records&assignees=cloin)してください。