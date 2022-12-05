---
slug: query-and-update-records
id: hoelh1ujyiqz
type: challenge
title: レコードのクエリーと更新
teaser: 複数タイプの複数レコードのクエリーと更新
注記:
- type: text
  コンテンツ: |-
    **ご存知ですか ?**
    Ansible コンテンツは読みやすく、プレーンテキストを使用しているため、Ansible を使用することでコードとしてのインフラストラクチャーを簡単に実現できます。
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
最後に、Web サーバーの再起動を阻んでいた架空の取締役会が終わったと仮定します。これで、変更要求を安全に実行し、インシデントと問題のステータスを更新してすべてが解決されたことを示すことができます。

これを実行するには、VS Code の `close-records-by-user.yml` Playbook を検証します。ここには、新しいモジュールがいくつかあります。これらの `*_info` モジュールは、ユーザー名で作成されたアクティブなレコードのさまざまなレコードタイプ (incident、problem、change_request) のクエリーに使用されています。その後、Ansible はこれらの返されたレコードを単純なオブジェクトリストに変換し、それぞれのモジュールに渡してレコードを更新/クローズします。モジュール自体によって実装されていないフィールドについては、特定のテーブルの他のフィールドまたはカスタムフィールドを指定するために使用できる `other` というモジュールパラメーターがあります。

この自動化を実行するには、以下を行います。
- automation controller のジョブテンプレート `4 - Query and close records by user (close-records-by-user.yml` を起動します。
- ジョブテンプレートの出力を監視し、ジョブが完了するまで待ちます。

ジョブが完了したら、以前の課題で作成したすべてのレコードをクローズまたは削除する必要があります。ジョブ出力には、クリーンアップされた関連するレコード番号がすべて表示されます。ServiceNow でビューを更新し、更新を確認します。

これですべてクリーンアップされました。次の課題に進んでください。