---
slug: env-overview
id: cw0l0swiz1du
type: challenge
title: 環境の概要
teaser: この課題では、ACME Corp 環境を確認します。
注記:
- type: text
  コンテンツ: "# ACME Corp.ダブリン工場とヨハネスブルグ工場\\n##### 工業用地
    は複雑なエコシステムであるため、工場長から \\U0001F50E\\U0001F4CA を監視して､
    生産ラインとパッケージ \\U0001F6E0\\U0001F4C8 を改善するように指示されました。実現するため､
    ACME は、HMI (Human Machine
    インターフェイス) ディスプレイに接続されています。\\n##### 一般的なユーザーには、キオスクモードで動作するアプリケーションを搭載したタブレットデバイス \\U0001F4F2 のように
    見えるでしょう (ビックリ!
     密かに稼動しているのは RHEL です)｡\\n#####  以下のような依存関係があります。
    IPAM、DNS 設定、ネットワーク接続、パッチ、ハードニングなどの依存関係は、並行して、または導入後の 2 日目のオペレーションとして解決する必要があります。
    \\n\\n<style type="text/css" rel="stylesheet">\\nh1,h2{\\n
    \\ text-align: center;\\n}\\np {\\n  text-align: center;\\n}\\nimg {\\n  display: block;\\n
    \\ margin-left: auto;\\n  margin-right: auto;\\n  height: 60%;\\n\\n}\\n</style>"
- type: text
  コンテンツ: "##### **Ansible Automation Platform** を使用した､
    コンテナー化されたアプリケーションとすべての依存関係のデプロイの自動化。 \\U0001F3C5\\U0001F3C5\\U0001F3C5\\n
    <center><img src=\"https://github.com/dafmendo/pictures_for_github/blob/fd9d1c424a130fbe4de73730b24d2a8c1d85e4bb/industrialapp-deploy-mesh.png?raw=true\"></center>\n
    Start ボタンをクリックして、このアドベンダーを開始します !\n\n<style type=\"text/css\"
    rel=\"stylesheet\">\nh1,h2{\n  text-align: center;\n}\np {\n  text-align: center;\n}\nimg
    {\n  display: block;\n  margin-left: auto;\n  margin-right: auto;\n  height: 60%;\n\n}\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: controller-edge-lab
  port: 443
難易度: 基本
時間制限: 600
---

🔐 ミッションのログイン認証情報
===

>**コントローラーのユーザー名**:
> ```yaml
>student
>```
>**コントローラーのパスワード**:
>```yaml
>learn_ansible
>```

👋 はじめに
===
### ACME Corp
ACME Corp は、Ansible Automation Platform を広範囲に使用して、複数のリージョンでエッジエコシステムを管理します。
この課題では、インストールを確認し、メッシュのワーカーノードタイプの詳細を確認し、コントローラーインスタンスおよびインスタンスグループを調べます。

##### ⏰ 推定所要時間: *10 分*

>**❗️注意**
>
>* ブラウザーの左上にある _Controller_ タブで、すべてのタスクを実行します。
>* 必要な場合は、提供された認証情報を使用して自動化コントローラーにログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。

☑️ 最初のタスク - ACME Corp オートメーションメッシュの概要
===

<a href="#mesh_nodes">
  <img alt="コントローラーログイン" src="../assets/img/mesh_nodes.png" />
</a>

<a href="#" class="lightbox" id="mesh_nodes">
  <img alt="Amesh_nodes" src="../assets/img/mesh_nodes.png" />
</a>

>ℹ️ 自動化メッシュは、TLS 接続を使用してネットワークオーバーレイを作成します。これは、以下に使用できるさまざまなワーカーノードタイプ間で確立されます。[コントロールプレーン](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#control_plane) と [実行プレーン](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#execution_plane) タスク。
>* **ハイブリッドノード** は、管理ジョブなどのコントロールプレーンタスクを実行し、自動化を実行できます。
>* **実行ノード** は自動化のみを実行し (Playbook を実行します)、プロジェクトの更新などの自動化コントローラーのランタイム機能は実行しません。

##### ACME Corp の自動化メッシュ設定とワーカーノードタイプ。

* `controller-edge-lab` \- ローリー本社にあり、*ハイブリッドノード* として設定されています。

* `jhb-edge-lab` \- ヨハネスブルグのリモート化学工場にあり、*実行ノード* として設定されています。

* `dublin-edge-lab` \- アイルランドの遠隔化学工場にあり、*実行ノード* として設定されています。

>**❗️注意**\
>自動化メッシュは、コントローラーのランタイムタスクのみを実行する **コントロール** ノードタイプと、*ジャンプホスト*のよに、実行またはコントロールプレーンタスクを実行せず、トラフィックを他の実行ノードにルーティングするだけの **ホップノード** も提供します。これらのノードは、このラボでは使用されません。

☑️ 2 番目のタスク - コントローラーインスタンスとインスタンスグループの概要
===

>ℹ️[インスタンスグループ](https://docs.ansible.com/automation-controller/latest/html/userguide/instance_groups.html) を使用すると、メッシュワーカーノードまたはインスタンスを論理的にグループ化し、ポリシーを適用してそれらの動作を決定できます。

##### ✏️ 自動化コントローラーのインスタンスグループを調べます。

* **Administration** セクションのサイドナビゲーションで、**Instance Groups** をクリックします。
* `default` インスタンスグループをクリックします。
* 上部の **Instances** タブをクリックします。`default` のインスタンスグループは、すべてのメッシュワーカーノードのデフォルトの場所であり、常にオートメーションコントローラーに存在します。これは、設定にインスタンスグループが指定されていない場合に *Job Template* を実行するために使用されます。

<a href="#default_ig">
  <img alt="Default IG" src="../assets/img/default_ig.png" />
</a>

<a href="#" class="lightbox" id="default_ig">
  <img alt="Defaul IG" src="../assets/img/default_ig.png" />
</a>


* `jhb-edge-lab` インスタンスをクリックし、*Node Type* を確認します。`jhb-edge-lab` は *実行ノード* として設定されます。

<a href="#jhb-exec">
  <img alt="JHB Exec ノード" src="../assets/img/jhb_exec_node.png" />
</a>

<a href="#" class="lightbox" id="jhb-exec">
  <img alt="ACME メッシュ" src="../assets/img/jhb_exec_node.png" />
</a>

* **Administration** セクションの **Instance Groups** をクリックして、メインのインスタンスグループウィンドウに戻ります。
* `controlplane` インスタンスグループをクリックします。
* 上部の **Instances** タブをクリックします。

<a href="#control_ig">
  <img alt="Control IG" src="../assets/img/control_ig.png" />
</a>

<a href="#" class="lightbox" id="control_ig">
  <img alt="Control IG" src="../assets/img/control_ig.png" />
</a>

>ℹ️ `controlplane` インスタンスグループは、[コントロールプレーン](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/red_hat_ansible_automation_platform_automation_mesh_guide/index#control_plane) タスクを実行するすべてのメッシュワーカーノードに対して事前に選択されたインスタンスグループです。

* `controller-edge-lab` インスタンスをクリックし、*Node Type* を確認します。`controller-edge-lab` は *ハイブリッドノード* として設定されます。

<a href="#hybrid_node">
  <img alt="Control IG" src="../assets/img/hybrid_node.png" />
</a>

<a href="#" class="lightbox" id="hybrid_node">
  <img alt="Control IG" src="../assets/img/hybrid_node.png" />
</a>

##### ✏️ ACME Corp インベントリーを見てみましょう

* 左側のナビゲーションバーの **Resources** メニューで、**Inventories** をクリックします。*ローリー DC* 本社、*ダブリン地域*、*ヨハネスブルグ地域* の 3 つの地域が表示されます。これらは、ヨーロッパとアフリカにある 2 つの工場に対応しています。

<a href="#inventories_regions">
  <img alt="inventories_regions" src="../assets/img/inventories_regions.png" />
</a>

<a href="#" class="lightbox" id="inventories_regions">
  <img alt="inventories_regions" src="../assets/img/inventories_regions.png" />
</a>

* *Dublin region* をクリックし`Dublin instance group` に割り当てられている、`Instance Groups` 値を確認します。

<a href="#inventories_dublinregion_instancegroup">
  <img alt="inventories_dublinregion_instancegroup" src="../assets/img/inventories_dublinregion_instancegroup.png" />
</a>

<a href="#" class="lightbox" id="inventories_dublinregion_instancegroup">
  <img alt="inventories_dublinregion_instancegroup" src="../assets/img/inventories_dublinregion_instancegroup.png" />
</a>

* 左側のナビゲーションバーの **Resources** メニューに戻り、**Inventories** をクリックします。**Inventroies** リストに再び戻ります。
* *Johannesburg region* をクリックし、`Johannessburg instance group` に割り当てられている `Instance Groups` の値に注目してください。

<a href="#inventories_jhbregion_instancegroup">
  <img alt="inventories_jhbregion_instancegroup" src="../assets/img/inventories_jhbregion_instancegroup.png" />
</a>

<a href="#" class="lightbox" id="inventories_jhbregion_instancegroup">
  <img alt="inventories_jhbregion_instancegroup" src="../assets/img/inventories_jhbregion_instancegroup.png" />
</a>

* 左側のナビゲーションバーの **Resources** メニューに戻り、**Inventories** をクリックします。**Inventroies** リストに再び戻ります。
* *Raleigh DC* をクリックし、`Raleigh data center` のインスタンスグループに割り当てられている `Instance Groups` の値を確認します。

☑️ 最終タスク - トポロジービューアーの使用
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

* 図の `jhb-edge-lab` ノードをクリックします。右上隅に、インスタンスの状態とメッシュノードタイプを表示できます。インスタンス名をクリックして、ノード設定にドリルダウンすることもできます。

<a href="#jhb_exec_topology">
  <img alt="jhb_exec_topology" src="../assets/img/jhb_exec_topology.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_topology">
  <img alt="jhb_exec_topology" src="../assets/img/jhb_exec_topology.png" />
</a>

✅ 次の課題
===
タスクを完了したら、下の `Next` ボタンを押して次のチャレンジに進みます。

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

