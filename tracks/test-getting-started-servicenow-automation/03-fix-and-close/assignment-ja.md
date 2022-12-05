---
slug: fix-and-close
id: uqqamri47d4n
type: challenge
title: 根本原因、修正、終了
teaser: 以前に作成したレコードのクエリーと新しい変更要求レコードのリンク
注記:
- type: text
  コンテンツ: |-
    **ご存知ですか ?**
    Ansible Playbook およびその他の Ansible コンテンツタイプは、通常、バージョン管理されたプレーンテキストとして保存されます。これは、継続的インテグレーションと継続的デプロイの一般的なアプローチが自動化コンテンツに簡単に適用できることを意味します。
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
ServiceNow の変更とは、過去または進行中のインシデントに関連する可能性のある問題に対処するための追加、削除、修正です。

`VS Code` タブに新しい Playbook が作成されました。
- 前と同じように、`change-attach.yml` という名前の新しい Playbook を確認します
- Automation controller で Resources > Job Templates に移動し、ジョブテンプレート 3 - Attach change request (change-attach.yml) を起動します
- Automation controller でジョブの完了を監視します。

ServiceNow に戻り、お気に入りの下にある `Change - Open` を選択します。これにより、作成されたすべての変更要求が一覧表示されます。`"Reboot the webserver"` というタイトルの新しい変更要求が作成され、表示されます。その他の関連フィールド (Description や On hold reason など) がどのように更新されたかにも注意してください。

以下の緑色の Next ボタンを選択して、次のセクションに移動します。