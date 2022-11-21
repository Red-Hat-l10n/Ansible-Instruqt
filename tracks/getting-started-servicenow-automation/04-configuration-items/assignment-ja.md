---
slug: configuration-items
id: a3tovyo45syj
type: challenge
title: ServiceNow CMDB のクエリーと更新
teaser: Ansible controller ワークフローを使用したノードファクトのクエリーと作成/更新
  CMDB の設定項目
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
ITIL では、設定管理データベース (CMDB) は組織がハードウェアおよびソフトウェアアセットを追跡するために使用するデータベースです。通常、ServiceNow CMDB は組織内の重要なサービスであり、多くの場合、IT アセットを追跡するための信頼できる唯一のソースと見なされます。

Ansible Automation Platform は、`servicenow.itsm` コレクション内のモジュールを利用して、ServiceNow の CMDB 内における設定アイテムのクエリーと更新を両方実行できます。

この課題では、2 つの Red Hat Enterprise Linux (RHEL) サーバーが自動的にプロビジョニングされ、Automation controller のインベントリーに追加されます。これらのホスト名は `node1` と `node2` です。`VS Code` タブに 2 つの Playbook が追加で作成されました。
- `collect-node-info.yml` は、これら 2 つの新しい RHEL ノードに関する情報を収集します。
- `create-update-config-items.yml` は収集したデータを使用して、CMDB の 2 つの新しい設定項目を作成または更新します。

ServiceNow フィルターナビゲーターボックスに Linux と入力して Linux 設定項目の現在のグループを表示し、`Configuration -> Servers -> Linux` をクリックして、Linux サーバーグループの設定項目リストを表示します。

![servicenow filter navigator](../assets/navigator-filter.jpg)

▶️ ノードのクエリーと CMDB の作成/更新
====
2 つの新しい Playbook が、自動化コントローラーで `4.0 - Query node info and update CMDB (multiple job templates)` と呼ばれる 1 つのワークフロージョブテンプレートに結合されました。
- この新しいワークフロージョブテンプレートの行には新しいボタンもあり、クリックすると、実行されるタスクがマップのノードとして視覚化されます。
- 新しいワークフロージョブテンプレートの起動
- ワークフローの実行中に任意のノードをクリックすると、ビジュアライザーの各ノードに対して起動された対応するジョブが表示されます。

🔍 検証結果
====
- ServiceNow フィルターナビゲーターボックスに Linux と入力して Linux 設定項目の更新されたグループを表示し、`Configuration -> Servers -> Linux` をクリックして、Linux サーバーグループの設定項目リストを表示します。
- 2 つの新しい設定項目が作成され、IP アドレスフィールドに設定項目が割り当てられていることに注意してください。

以下の緑色の Next ボタンを選択して、次のセクションに移動します。

NORMAL で問題が発生していますか ?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] してください (https://github.com/ansible/instruqt/issues/new?labels=getting-started-servicenow-automation&title=New+servicenow+issue:+configuration-items&assignees=cloin)。