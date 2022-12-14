---
slug: edge-workflow
id: v6imeyyvddqv
type: challenge
title: コントローラーのワークフローを使用してプロセスを簡素化する
teaser: すべてを自動化!
注記:
- type: text
  コンテンツ: "# ファイナルミッション: なぜ複数回クリック?どのようにスケーリングできますか?\\n##### 
    Ignitionアプリケーション \\U0001F4F2、監視アプリケーション \\U0001F50E、およびファイアウォール設定をグローバルに展開するための
    ワークフロージョブテンプレートを設定します。\\U0001F50E.\\n#####
    これには、オートメーションメッシュを使用するヨハネスブルグ工場の HMI デバイスが含まれるようになりました。\\n#####
    このアドベンチャーを始めるには、Start ボタンをクリックしてください!n\\n<style type="text/css" rel="stylesheet">\\nh1,h2{\\n
    \\ text-align: center;\\n}\\np {\\n  text-align: center;\\n}\\nimg {\\n  display: block;\\n
    \\ margin-left: auto;\\n  margin-right: auto;\\n  height: 60%;\\n\\n}\\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: controller-edge-lab
  port: 443
- title: Jhb アプリ
  type: service
  hostname: jhb-edge-lab
  path: /web/login
  port: 8088
  new_window: true
- title: Jhb mon
  type: service
  hostname: jhb-edge-lab
  path: /network
  port: 9090
  url: https://jhb-edge-lab:9090
  new_window: true
- title: Dublin アプリケーション
  type: service
  hostname: dublin-edge-lab
  path: /web/login
  port: 8088
  new_window: true
- title: Dublin mon
  type: service
  hostname: dublin-edge-lab
  path: /network
  port: 9090
  url: https://dublin-edge-lab:9090
  new_window: true
難易度: 基本
時間制限: 600
---

🔐 ミッションのログイン認証情報
===

>**コントローラーおよびモニターリングのユーザー名**:
> ```yaml
>student
>```
>**コントローラーおよびモニターリングパスワード**:
>```yaml
>learn_ansible
>```

>**Ignition ユーザー名**:
> ```yaml
>admin
>```
>**Ignition パスワード**:
>```yaml
>learn_ansible
>```

👋 はじめに
===
# 最終ミッション: オーケストレーション!ヨハネスブルグ工場を設定する
Ignition アプリケーション、監視ダッシュボード、およびファイアウォールセキュリティー設定をグローバルにデプロイします。これには、オートメーションメッシュを使用するヨハネスブルグ工場の HMI デバイスが含まれるようになりました。
複数の地域で複数の自動化ジョブを実行し、事前定義された条件に従うことで、自動化を調整します。

##### ⏰ 推定所要時間: *10 分*

>**❗️注意**
>
>* 必要な場合は、_Controller_ タブから提供された認証情報を使用して自動化コントローラーにログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。
>* 以下は、この例で使用されている Playbook への [リンク](https://github.com/craig-br/instruqt-track-content/tree/devel/getting-started-edge-lab/playbooks) です。
* ワークフローの手順をスキップする場合。**Resource** セクションで **Templates** をクリックすると、次の名前の `Job Template` が表示されます。`ヘルプ!エッジワークフローを作成`します｡<img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" />アイコンをクリックして、ワークフロー設定をデプロイします。
<a href="#help-wf">
  <img alt="自動導入ワークフロー" src="../assets/img/help-wf.png" />
</a>

<a href="#" class="lightbox" id="help-wf">
  <img alt="自動導入ワークフロー" src="../assets/img/help-wf.png" />
</a>

☑️ 最初のタスク - Global スマートインベントリーを探索する
===

##### ✏️ **automation controller** で *Global* インベントリーを探索します。

* **Resources** セクションの下のサイドナビゲーションで、**Inventories** をクリックします｡
* スマートインベントリーである 3 つの `Global` インベントリーがあることを確認します。

ℹ️スマートインベントリーは、保存された検索語に基づいてデバイスをフィルタリングします。詳細は、[公式ドキュメント](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html#smart-inventories) を参照してください。
<a href="#global-inventories">
  <img alt="Global イベントリー" src="../assets/img/global-inventories.png" />
</a>

<a href="#" class="lightbox" id="global-inventories">
  <img alt="Global イベントリー" src="../assets/img/global-inventories.png" />
</a>

* `Global edge firewalls` インベントリーをクリックすると、`Smart host filter` を使用して、このインベントリーのダブリンとヨハネスブルグからファイアウォールホストが読み込まれることに注意してください。
ℹ️ `Smart host filters` の詳細は、[公式ドキュメント](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html) を参照してください。

<a href="#global-edge-firewalls">
  <img alt="Global edge firewalls" src="../assets/img/global-edge-firewalls.png" />
</a>

<a href="#" class="lightbox" id="global-edge-firewalls">
  <img alt="Global edge firewalls" src="../assets/img/global-edge-firewalls.png" />
</a>

* **Hosts** タブに入力された、フィルタリングされたホストを確認できます。

<a href="#global-edge-firewalls-hosts">
  <img alt="Global edge firewalls hosts" src="../assets/img/global-edge-firewalls-hosts.png" />
</a>

<a href="#" class="lightbox" id="global-edge-firewalls-hosts">
  <img alt="Global edge firewalls hosts" src="../assets/img/global-edge-firewalls-hosts.png" />
</a>

**Inventories** に戻り、`Global monitoring devices` と `Global kiosk devices` に対して同じ手順を繰り返します。インベントリーは、ホストをグループ化するために異なるスマートフィルターを使用していることに注意してください。

☑️ 2 番目のタスク - アプリケーションと監視ダッシュボードのデプロイメントとセキュリティー設定を調整する
===
##### *Global edge configuration* ワークフローテンプレートを作成します。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Add` ボタンをクリックし、ドロップダウンメニューから `Add workflow template` を選択します。

<a href="#add_workflow_template">
  <img alt="Add workflow template" src="../assets/img/add_workflow_template.png" />
</a>

<a href="#" class="lightbox" id="add_workflow_template">
  <img alt="Add workflow template" src="../assets/img/add_workflow_template.png" />
</a>

以下の設定を使います｡
>**Name**:
> ```yaml
>Global edge configuration
>```
>**Organization**:
>```yaml
>ACME Corp
>```

<a href="#wf-settings">
  <img alt="Workflow-settings" src="../assets/img/wf-settings.png" />
</a>

<a href="#" class="lightbox" id="wf-settings">
  <img alt="Workflow-settings" src="../assets/img/wf-settings.png" />
</a>

`Save` ボタンをクリックすると、`Visualizer` ウィンドウが自動的に開きます。

* `Start` ボタンをクリックして開始します

<a href="#wf-start">
  <img alt="ワークフローを開始" src="../assets/img/wf-start.png" />
</a>

<a href="#" class="lightbox" id="wf-start">
  <img alt="ワークフローを開始" src="../assets/img/wf-start.png" />
</a>

☑️ 2.1.ワークフローに Deploy edge application ノードを追加する
===
* `Add Node` ウィンドウで `Deploy edge application` ジョブテンプレートを選択し、`Next` をクリックします。

<a href="#add-node-deploy-edge-app">
  <img alt="Deploy edge application ノードの追加" src="../assets/img/add-node-deploy-edge-app.png" />
</a>

<a href="#" class="lightbox" id="add-node-deploy-edge-app">
  <img alt="Deploy edge application ノードの追加" src="../assets/img/add-node-deploy-edge-app.png" />
</a>

* `Global kiosk devices` インベントリーを選択し、`Next` をクリックします。
<a href="#global-kiosk-inventory-wf">
  <img alt="Global kiosk devices inventory" src="../assets/img/global-kiosk-inventory-wf.png" />
</a>

<a href="#" class="lightbox" id="global-kiosk-inventory-wf">
  <img alt="Global kiosk devices inventory" src="../assets/img/global-kiosk-inventory-wf.png" />
</a>

* `Save` をクリックします｡
<a href="#preview-deployedgeapplication">
  <img alt="エッジアプリのでデプロイプレビュー" src="../assets/img/preview-deployedgeapplication.png" />
</a>

<a href="#" class="lightbox" id="preview-deployedgeapplication">
  <img alt="エッジアプリのでデプロイプレビュー" src="../assets/img/preview-deployedgeapplication.png" />
</a>


☑️ 2.2.ワークフローに Deploy monitoring ダッシュボードノードを追加する
===
* 前の手順で `Save` をクリックすると、`Visualizer` ウィンドウに戻ります。青い `Start` ボタンの横にある `+` をクリックします。

<a href="#deploy-edge-app-plus">
  <img alt="Deploy edge aplication plus" src="../assets/img/deploy-edge-app-plus.png" />
</a>

<a href="#" class="lightbox" id="deploy-edge-app-plus">
  <img alt="Deploy edge aplication plus" src="../assets/img/deploy-edge-app-plus.png" />
</a>

* `Deploy monitoring dashboards` ジョブテンプレートを選択します。準備が整ったら `Next` をクリックします。
<a href="#deploy-mondash-wf">
  <img alt="Add Deploy monitoring dashboards Node" src="../assets/img/deploy-mondash-wf.png" />
</a>

<a href="#" class="lightbox" id="deploy-mondash-wf">
  <img alt="Add Deploy monitoring dashboards Node" src="../assets/img/deploy-mondash-wf.png" />
</a>

* `Global monitoring devices` インベントリーを選択し、`Next` をクリックします。
<a href="#deploy-mondash-inventory-wf">
  <img alt="Global monitoring devices inventory" src="../assets/img/deploy-mondash-inventory-wf.png" />
</a>

<a href="#" class="lightbox" id="deploy-mondash-inventory-wf">
  <img alt="Global monitoring devices inventory" src="../assets/img/deploy-mondash-inventory-wf.png" />
</a>

* `Save` をクリックします｡
<a href="#deploy-mondash-preview-wf">
  <img alt="Preview deploy monitoring dashboards" src="../assets/img/deploy-mondash-preview-wf.png" />
</a>

<a href="#" class="lightbox" id="deploy-mondash-preview-wf">
  <img alt="Preview deploy monitoring dashboards" src="../assets/img/deploy-mondash-preview-wf.png" />
</a>

☑️ 2.3.ワークフローに Configure edge firewalls ノードを追加する
===
* `Visualizer` から `Deploy monitoring dashboard` ボタンをクリックし、`+` アイコンをクリックします。
<a href="#deploy-fw-plus">
  <img alt="Add firewall node" src="../assets/img/deploy-fw-plus.png" />
</a>

<a href="#" class="lightbox" id="deploy-fw-plus">
  <img alt="Add firewall node" src="../assets/img/deploy-fw-plus.png" />
</a>

* `On Success` 条件を選択し、`Next` をクリックします。
<a href="#rule-onsuccess">
  <img alt="On Success" src="../assets/img/rule-onsuccess.png" />
</a>

<a href="#" class="lightbox" id="rule-onsuccess">
  <img alt="On Success" src="../assets/img/rule-onsuccess.png" />
</a>

* ジョブテンプレート `Configure edge firewalls` を選択し、`Next` をクリックします。
<a href="#config_fw_node">
  <img alt="Configure edge firewalls Node" src="../assets/img/config_fw_node.png" />
</a>

<a href="#" class="lightbox" id="config_fw_node">
  <img alt="Configure edge firewalls Node" src="../assets/img/config_fw_node.png" />
</a>

* `Global edge firewalls` インベントリーを選択し、`Next` をクリックします。
<a href="#config-fw-inventory-wf">
  <img alt="Global edge firewalls inventory" src="../assets/img/config-fw-inventory-wf.png" />
</a>

<a href="#" class="lightbox" id="config-fw-inventory-wf">
  <img alt="Global edge firewalls inventory" src="../assets/img/config-fw-inventory-wf.png" />
</a>

* `Save` をクリックします｡
<a href="#config-fw-preview-wf">
  <img alt="Preview configure firewalls" src="../assets/img/config-fw-preview-wf.png" />
</a>

<a href="#" class="lightbox" id="config-fw-preview-wf">
  <img alt="Preview configure firewalls" src="../assets/img/config-fw-preview-wf.png" />
</a>

☑️ 2.4.Global edge configuration ワークフローを保存すいる
===
* `Visualizer` から、右上にある `Save` ボタンをクリックします。
<a href="#wf-save">
  <img alt="Save workflow" src="../assets/img/wf-save.png" />
</a>

<a href="#" class="lightbox" id="wf-save">
  <img alt="Save workflow" src="../assets/img/wf-save.png" />
</a>

☑️ 3 番目のタスク - Global edge configuration ワークフローを起動する
===
##### ✏️ *Global edge configuration* ワークフローテンプレートを起動します。
* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Global edge configuration` <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックして、ワークフローテンプレートを起動します。
* ワークフローが自動的に実行され、**Views** - **Jobs** タブにリダイレクトされ、ライブ実行を観察できます。

<a href="#wf-run">
  <img alt="Global edge configuration execution" src="../assets/img/wf-run.png" />
</a>

<a href="#" class="lightbox" id="wf-run">
  <img alt="Global edge configuration execution" src="../assets/img/wf-run.png" />
</a>

* 完了すると、各 `Job Template` に対応する各ノードが強調表示され、実行にかかった時間が表示されます。

<a href="#wf-finalized">
  <img alt="Workflow finalized" src="../assets/img/wf-finalized.png" />
</a>

<a href="#" class="lightbox" id="wf-finalized">
  <img alt="Workflow finalized" src="../assets/img/wf-finalized.png" />
</a>

☑️ 最終タスク - 機能するかどうかをテストします!
===
* `Jhb app`、`Jhb mon`、`Dublin app` および `Dublin mon` タブをクリックして、monitoring ダッシュボードとアプリケーションにログインしてください。

<a href="#Dublin and Johannessburg tabs">
  <img alt="Dublin と Johannessburg タブ" src="../assets/img/apps-mondash.png" />
</a>

<a href="#" class="lightbox" id="Dublin and Johannessburg tabs">
  <img alt="Dublin と Johannessburg タブ" src="../assets/img/apps-mondash.png" />
</a>

* すべての場所の monitoring ダッシュボードとアプリケーションが利用可能である必要があります。対応する認証情報でログインします。

✅ チャレンジをチェック
===
以下の `Check` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

NORMAL で問題が発生していますか ?
====
問題が発生した場合や、何かがおかしいと気付いた場合は、[チケットを作成](https://github.com/ansible/instruqt/issues/new?labels=getting-started-edge-lab&title=Getting+started+with+Ansible+Automation+Platform+and+edge+issue:+incident-creation&assignees=dafmendo) してください。

<style type="text/css" rel="stylesheet">
  .lightbox {
    display: none;
    position: fixed;
    justify-content: center;
    align-items: center;
    z-index: 999;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 1rem;
    background: rgba(0, 0, 0, 0.8);
    margin-left: auto;
    margin-right: auto;
    margin-top: auto;
    margin-bottom: auto;
  }
  .lightbox:target {
    display: flex;
  }
  .lightbox img {
    max-width: 60%;
    max-height: 60%;
  }
  img {
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 100%;
  }
  h1 {
    font-size: 18px;
  }
    h2 {
    font-size: 16px;
    font-weight: 600
  }
    h3 {
    font-size: 14px;
    font-weight: 600
  }
  p span {
    font-size: 14px;
  }
  ul li span {
    font-size: 14px
  }
</style>