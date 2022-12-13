---
slug: incident-creation
id: ty5jkjlendod
type: challenge
title: インシデントの作成
teaser: インシデント作成の自動化
注記:
- type: text
  コンテンツ: |-
    <p align="center">
    <img width="400" src="../assets/snow-aap.png">
    </p>
    Ansible Automation Platform の ServiceNow 統合が、
    `servicenow.itsm` と呼ばれる認定コンテンツコレクションを使用することで可能になりました。 このコレクションは、
    `console.redhat.com` の Automation Hub で利用できます。作成中の環境では、
    実行環境にこのコレクションが含まれ、
    Ansible Automation Platform は ServiceNow インスタンスに対して
    タスクを実行できます。
- type: text
  コンテンツ: |-
    この学習トラックでは、この統合のコア機能を説明します。

    この学習トラックで問題が発生した場合は、Github ページで新しいチケットを作成してください: https://github.com/ansible/instruqt/issues
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
ITIL において、インシデントは IT サービスまたはアプリケーションの計画外の停止または品質低下を指します。ServiceNow は、ITIL 用語にマッピングされたテクノロジーを実装しており、インシデント管理の業界標準として受け入れられています。

servicenow.itsm 認定コレクションを使用すると、組織は Ansible Automation Platform ワークフロー内のインシデント管理を利用できます。

`VS Code` タブで作成された、`incident-create.yml` と呼ばれる playbook。
- この playbook を検証してインラインコメントを確認し、コレクションがどのように活用されているか確認します。

▶️ インシデントの作成
====
- 次に、`readme.md` で指定されたログイン認証情報を使用して、Automation Controller タブにアクセスします。

- `Resources > Templates` に移動し、ロケットアイコンをクリックして `1 - Create incident (incident-create.yml)` ジョブを起動します。
![launch job icon](../assets/launch-icon.png)

🔍 検証結果
====

前の手順が正常に完了していれば、新規インシデントが作成されています。これを確認するには、以下を実行します。
- `readme.md` の ServiceNow 認証情報を使用して、`ServiceNow` タブから ServiceNow にアクセスします。

- ServiceNow で、星のアイコンをクリックして事前設定済みのお気に入りにアクセスし、`Self-service - Incidents` を選択します:
![servicenow screenshot](../assets/snow-star.png)


これで新規インシデントが作成されました。自分で作成したことを確認するには、上記の手順とスクリーンショットに従い、新しく作成したインシデントにアクセスします。この環境の一意のユーザー名は、インシデントの説明に表示されます。インシデント番号は、Automation Controller 内のジョブ実行出力に表示されるインシデント番号とも一致する必要があります。

以下の緑色の Next ボタンを選択して、次のセクションに移動します。

🐛 問題が発生しましたか?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] してください (https://github.com/ansible/instruqt/issues/new?labels=getting-started-servicenow-automation&title=New+servicenow+issue:+incident-creation&assignees=cloin)。