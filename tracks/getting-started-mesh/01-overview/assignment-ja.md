---
slug: overview
id: prkjjelykzcb
type: challenge
title: Automation Mesh の概要
teaser: Automation Mesh の概念の確認
注記:
- type: text
  コンテンツ: "# \\U0001F50E ACME Corp environment overview\\n\\n![node_overview](../assets/img/mesh_nodes.png)\\n\\nIn
    この課題では、ACME Corp 環境と設定について確認します。\\n\\n<style
    type="text/css" rel="stylesheet">\\nh1,h2{\\n  text-align: center;\\n}\\np {¨\\n
    \\ text-align: center;\\n}\\nimg {\\n  display: block;\\n  margin-left: auto;\\n  margin-right:
    auto;\\n  height: 60%;\\n\\n}\\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: raleigh-controller
  port: 443
難易度: 基本
制限時間: 300
---

🔐 ログイン認証情報
===
すべてのログインで同じ認証情報が使用されます。

>**ユーザー名**:
> ```yaml
>student
>```
>**パスワード**:
>```yaml
>learn_ansible
>```

👋 はじめに
===

##### ⏰ 推定所要時間: *5 分*

ACME Corp は、Ansible Automation Platform を広範囲に使用して、複数のリージョンで IT エコシステムを管理します。 この課題では、インストールを確認し、メッシュのワーカーノードタイプの詳細を確認し、コントローラーインスタンスおよびインスタンスグループを調べます。

>**❗️注意**
>
>* ブラウザーの左上にある _Controller_ タブで、すべてのタスクを実行します。
>* 必要な場合は、提供された認証情報を使用してAutomation Controller にログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。

☑️ タスク - ACME Corp メッシュの概要
===

<a href="#mesh_nodes">
  <img alt="コントローラーログイン" src="../assets/img/mesh_nodes.png" />
</a>

<a href="#" class="lightbox" id="mesh_nodes">
  <img alt="Amesh_nodes" src="../assets/img/mesh_nodes.png" />
</a>

>ℹ️ Automation Mesh には [コントロールプレーン](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#control_plane) および [実行プレーン](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#execution_plane) タスクに使用できるさまざまなワーカーノードのタイプがあります。
>* **ハイブリッドノード** は、管理ジョブなどのコントロールプレーンタスクを実行し、自動化を実行できます。
>* **実行ノード** は自動化のみを実行し (Playbook の実行)、プロジェクトの更新などの Automation Controller のランタイム機能は実行しません。
>* ジャンプホストと同様に、**ホップノード** では実行またはコントロールプレーンのタスクは実行されません。トラフィックを他の実行ノードにのみルーティングします。

##### ACME Corp の Automation Mesh 設定とワーカーノードタイプ。

* `Raleigh-controller`: Raleigh のデータセンターに配置されており、**hybrid node** として設定されています。

* `jhb-exec`: Johannesburg のリモートオフィスに配置されており、**実行ノード** として設定されます。

* `Dublin-hop` \- Irish パブリッククラウドリージョンで、**ホップノード** として設定されています。`Dublin-hop` は *inactive* であり、バックアップワーカーノードが必要な場合にのみ有効になります。これについては、後のタスクで説明します。

>**❗️注意**\
>Automation Mesh は、コントローラーランタイムタスクのみを実行する **コントロール** ノードタイプも含まれます。自動化の実行は無効になっています。これらのノードは、このラボでは使用されません。

☑️ タスク: コントローラーインスタンスおよびインスタンスグループ
===

>ℹ️[インスタンスグループ](https://docs.ansible.com/automation-controller/latest/html/userguide/instance_groups.html) を使用すると、メッシュワーカーノードまたはインスタンスを論理的にグループ化し、ポリシーを適用してそれらの動作を決定できます。

##### ✏️ Automation Controller のインスタンスグループを調べます。

* 指定の認証情報を使用してAutomation Controller にログインします。
* **Administration** セクションのサイドナビゲーションで、**Instance Groups** をクリックします。
* `default` インスタンスグループをクリックします。
* 上部の **Instances** タブをクリックします。

<a href="#default_ig">
  <img alt="デフォルト IG" src="../assets/img/default_ig.png" />
</a>

<a href="#" class="lightbox" id="default_ig">
  <img alt="Defaul IG" src="../assets/img/default_ig.png" />
</a>

`default` のインスタンスグループは、すべてのメッシュワーカーノードのデフォルトの場所であり、常にオートメーションコントローラーに存在します。これは、設定にインスタンスグループが指定されていない場合に *ジョブテンプレート* を実行するために使用されます。

>**❗️注意**\
>**ホップノード** は自動化ジョブを実行せず、インスタンスグループには割り当てられません。

* `jhb-exec` インスタンスをクリックし、`ノードタイプ` を確認します。`jhb-exec` は **実行ノード** として設定されます。

<a href="#jhb-exec">
  <img alt="JHB Exec ノード" src="../assets/img/jhb_exec_node.png" />
</a>

<a href="#" class="lightbox" id="jhb-exec">
  <img alt="ACME メッシュ" src="../assets/img/jhb_exec_node.png" />
</a>

* **Administration** セクションの **Instance Groups** をクリックして、メインのインスタンスグループウィンドウに戻ります。
* `controlplane` インスタンスグループをクリックします。
* 上部の `Instances` タブをクリックします。

<a href="#control_ig">
  <img alt="Control IG" src="../assets/img/control_ig.png" />
</a>

<a href="#" class="lightbox" id="control_ig">
  <img alt="Control IG" src="../assets/img/control_ig.png" />
</a>

>ℹ️ `controlplane` インスタンスグループは、[コントロールプレーン](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#control_plane) タスクを実行するすべてのメッシュワーカーノードに対して事前に選択されたインスタンスグループです。

* `raleigh-controller` インスタンスをクリックし、**ノードタイプ** を確認します。`Raleigh-controller` は **ハイブリッドノード** として設定されます。

<a href="#hybrid_node">
  <img alt="Control IG" src="../assets/img/hybrid_node.png" />
</a>

<a href="#" class="lightbox" id="hybrid_node">
  <img alt="Control IG" src="../assets/img/hybrid_node.png" />
</a>

☑️ タスク - トポロジービューアーの使用
===
>ℹ️[トポロジービューアー](https://docs.ansible.com/automation-controller/latest/html/administration/topology_viewer.html) は、オートメーションメッシュ用の視覚的でインタラクティブなダッシュボードです。これは、メッシュトポロジーのノードタイプ、ヘルス、および詳細のビューを提供します。

##### ✏️ トポロジービューアーで ACME Corp のメッシュデザインを表示してみましょう。

* 左側のナビゲーションバーの **Administration** メニューで、**Topology View** をクリックします。

<a href="#topology_viewer">
  <img alt="topology_viewer" src="../assets/img/topology_viewer.png" />
</a>

<a href="#" class="lightbox" id="topology_viewer">
  <img alt="topology_viewer" src="../assets/img/topology_viewer.png" />
</a>

>**❗️注意**\
>`dublin-hop` ノードは現在エラーステータスを示しています。
>ACME Corp は、バックアップとしてのみ使用されるため、`dublin-hop` を意図的に *inactive* にします。この機能は、このラボの後半で説明します。

* 図の `jhb-exec` ノードをクリックします。

<a href="#jhb_exec_topology">
  <img alt="jhb_exec_topology" src="../assets/img/jhb_exec_topology.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_topology">
  <img alt="jhb_exec_topology" src="../assets/img/jhb_exec_topology.png" />
</a>

トポロジービューアーは、インスタンスの正常性ステータスを簡単に表示するための簡単な方法です。右上隅に、インスタンスの状態とメッシュノードタイプを表示できます。

インスタンス名をクリックして、ノード設定にドリルダウンすることもできます。

✅ 次の課題
===
タスクを完了したら、下の `Next` ボタンを押して次のチャレンジに進みます。

🐛 問題が発生していますか ?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] してください (https://github.com/ansible/instruqt/issues/new?labels=getting-started-mesh&title=Getting+started+with+automation+mesh+issue&assignees=craig-br)。

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
