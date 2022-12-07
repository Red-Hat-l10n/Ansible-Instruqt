---
slug: multi-site
id: syfkcfuon0qw
type: challenge
title: メッシュを使用したマルチサイトの自動化
teaser: Automation Mesh を使用した複数のサイトでの自動化ジョブ実行
注記:
- type: text
  コンテンツ: "# \\U0001F44B ACME Corp インベントリーへのインスタンスグループの割り当て\\n\\n![node_overview](../assets/img/instance_groups_main.png)\\n\\nIn
    この課題により、メッシュ実行ノードを異なるリージョンに割り当てます。
    インスタンスグループを ACME Corp コントローラーインベントリーに関連付けます。\\n\\n<style type="text/css"
    rel="stylesheet">\\nh1,h2{\\n  text-align: center;\\n}\\np {\\n  text-align: center;\\n}\\nimg
    {\\n  display: block;\\n  margin-left: auto;\\n  margin-right: auto;\\n  height: 60%;\\n\\n}\\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: raleigh-controller
  port: 443
難易度: 基本
制限時間: 600
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

#### ⏰ 推定所要時間: 10 分

Raleigh リージョンおよび Johannesburg リージョンのインスタンスグループを作成し、対応するインスタンスを関連付けたので、これらのインスタンスグループを適切な ACME Corp コントローラー [インベントリー](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html)に割り当てることができます。

>**❗️注意**
>* ブラウザーの左上にある _Controller_ タブで、すべてのタスクを実行します。
>* 必要な場合は、提供された認証情報を使用してAutomation Controller にログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。

☑️ タスク - インベントリーへのインスタンスグループの割り当て
===

>ℹ️ インスタンスグループおよび関連するメッシュワーカーノードは、_組織_ の、_インベントリー_、および _ジョブテンプレート_ などのAutomation Controller オブジェクトに割り当てられます。

ACME Corp は、最新のメッシュワーカーノードがそれぞれの環境で自動化を実行することを確認するために、Johannesburg および Raleigh の場所に正しいインスタンスグループを割り当てる必要があります。

##### ✏️ `Raleigh data center` インスタンスグループと `Raleigh DC` インベントリーを関連付けましょう。

* **Resources** セクションの下のサイドナビゲーションで、**Inventories** をクリックします
* `Raleigh DC inventory` をクリックします。
* **Edit** をクリックします。
* **Instance Groups** の拡大鏡ボタンをクリックします。
* **Raleigh data center** の横にあるボックスにチェックを入れます。
* **Select** をクリックします。
* **Edit Details** ウィンドウで **Save** をクリックします。

<a href="#raleigh_inv_ig">
  <img alt="raleigh_inv_ig" src="../assets/img/raleigh_inv_ig.png" />
</a>

<a href="#" class="lightbox" id="raleigh_inv_ig">
  <img alt="raleigh_inv_ig" src="../assets/img/raleigh_inv_ig.png" />
</a>

#####  `Johannesburg data center` インスタンスグループと `Johannesburg DC inventory` に対して同じ作業を行います。

* **Resources** セクションの下のサイドナビゲーションで、**Inventories** をクリックします
* `Johannesburg DC` インベントリーをクリックします。
* **Edit** をクリックします。
* **Instance Groups** の _拡大鏡ボタン_ をクリックします。
* **Johannesburg data center** の横にあるボックスにチェックを入れます。
* **Select** をクリックします。
* **Edit Details** ウィンドウで **Save** をクリックします。

<a href="#jhb_inv_ig">
  <img alt="jhb_inv_ig" src="../assets/img/jhb_inv_ig.png" />
</a>

<a href="#" class="lightbox" id="jhb_inv_ig">
  <img alt="jhb_inv_ig" src="../assets/img/jhb_inv_ig.png" />
</a>

☑️ タスク - 自動化を実行する場所の選択
===

ACME Corp IT は、Web サイトの応答に時間がかかると報告を受けました。Johannesburg リモートオフィスおよび Raleigh データセンター内の Red Hat Enterprise Linux (RHEL) インスタンスからシステム情報を収集する必要があります。

これらは、事前に作成された `Debug info` [job template] (https://docs.ansible.com/automation-controller/latest/html/userguide/job_templates.html) を使用して情報収集および障害検出を行います。

##### ✏️ Raleigh データセンターで `Debug info` ジョブテンプレートを実行しましょう。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Debug info ジョブ` テンプレート行の **Actions** 列にある <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックします。これにより、新しいウィンドウが開きます。

<a href="#debug_info_raleigh">
  <img alt="debug_info_raleigh" src="../assets/img/debug_info_raleigh.png" />
</a>

<a href="#" class="lightbox" id="debug_info_raleigh">
  <img alt="debug_info_raleigh" src="../assets/img/debug_info_raleigh.png" />
</a>

>**❗️注意**
>
>`Debug info` ジョブテンプレートは、起動前にどのインベントリーを使用するかを確認するように設定されています。ジョブテンプレートは、実行前に特定のパラメーターについてユーザー入力を要求する機能を提供します。これは、複数の ACME Corp インベントリーで自動化を実行する必要がある場合に便利です。

* `Raleigh DC` インベントリーを選択したままにします。
* **Next** をクリックし、**Launch** をクリックします。これにより、*Job Output* ウィンドウが開きます。

<a href="#debug_info_raleigh_details">
  <img alt="debug_info_raleigh_details" src="../assets/img/debug_info_raleigh_details.png" />
</a>

<a href="#" class="lightbox" id="debug_info_raleigh_details">
  <img alt="debug_info_raleigh_details" src="../assets/img/debug_info_raleigh_details.png" />
</a>

* ウィンドウの上部にある **Details** タブをクリックします。

`Raleigh data center` インスタンスグループおよび `raleigh-controller` インスタンスを使用してジョブを実行することに注意してください。

##### 次に、Johannesburg リージョンで `Debug info` ジョブテンプレートを実行します。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Debug info` ジョブテンプレート行の _Actions_ 列にある <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックします。これにより、新しいウィンドウが開きます。

<a href="#debug_info_jhb_inv">
  <img alt="debug_info_jhb_inv" src="../assets/img/debug_info_jhb_inv.png" />
</a>

<a href="#" class="lightbox" id="debug_info_jhb_inv">
  <img alt="debug_info_jhb_inv" src="../assets/img/debug_info_jhb_inv.png" />
</a>

* `Johannesburg DC` インベントリーを選択します。
* **Next** をクリックし、**Launch** をクリックします。これにより、*Job Output* ウィンドウが開きます。
* 前述の手順で行ったように、ウィンドウの上部にある **Details** タブをクリックします。

<a href="#debug_info_jhb_details">
  <img alt="debug_info_jhb_details" src="../assets/img/debug_info_jhb_details.png" />
</a>

<a href="#" class="lightbox" id="debug_info_jhb_details">
  <img alt="debug_info_jhb_details" src="../assets/img/debug_info_jhb_details.png" />
</a>

`Johannesburg data center` インスタンスグループと `jhb-exec` インスタンスを使用してジョブを実行することに注意してください。

☑️ タスク - 詳細の確認 - メッシュオーバーレイネットワーク
===

リモートワーカーノードへの到達に使用されるルートAutomation Mesh を確認し、`Debug info` ジョブテンプレートを実行していきましょう。

`Mesh route info` ジョブテンプレートは、Automation Mesh の `receptorctl` コマンドラインツールを使用して、Johannesburg リモートオフィスの `jhb-exec` ワーカーノードのステータスを返します。ジョブテンプレートには、自動化ジョブが情報収集時に使用したパスも表示されます。

##### ✏️ では、`Mesh route info` ジョブテンプレートを使用して、Raleigh データセンターから `jhb-exec` へのルートを見てみましょう。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Mesh route info` ジョブテンプレート行の _Actions_ 列の下にある <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックします。

<a href="#route_info_launch">
  <img alt="route_info_launch" src="../assets/img/route_info_launch.png" />
</a>

<a href="#" class="lightbox" id="route_info_launch">
  <img alt="route_info_launch" src="../assets/img/route_info_launch.png" />
</a>

* これにより、新しいウィンドウが開きます。`Raleigh DC` インベントリーを選択したままにします。
* **Next** をクリックし、**Launch** をクリックします。

`Output` ウィンドウで、すべてのタスクが成功したことを確認します。

<a href="#mesh_route_raleigh_path">
  <img alt="mesh_route_raleigh_path" src="../assets/img/mesh_route_raleigh_path.png" />
</a>

<a href="#" class="lightbox" id="mesh_route_raleigh_path">
  <img alt="mesh_route_raleigh_path" src="../assets/img/mesh_route_raleigh_path.png" />
</a>

メッシュノードタスクへの _Print_ パスで、パスの最初のホップが `raleigh-controller` で、その後に `jhb-exec` に到達する点に注意してください。これは、ジョブが Raleigh で開始され、`raleigh-controller` ハイブリッドノードを使用して `jhb-exec` 実行ノードに接続したことを示しています。

##### 次に、`Johannesburg DC` インベントリーを使用して `Mesh route info` ジョブテンプレートを実行します。

* 上記の手順に従って、`Mesh route info` ジョブテンプレートを実行します。
* 今回は、`Johannesburg DC` インベントリーを選択します。
* **Next** をクリックし、**Launch** をクリックします。

<a href="#mesh_route_jhb_path">
  <img alt="mesh_route_jhb_path" src="../assets/img/mesh_route_jhb_path.png" />
</a>

<a href="#" class="lightbox" id="mesh_route_jhb_path">
  <img alt="mesh_route_jhb_path" src="../assets/img/mesh_route_jhb_path.png" />
</a>

Johannesburg リモートオフィスで自動化を開始したので、メッシュノードへの _Print_ パスで、`jhb-exec` への到達に追加のホップが必要ない点に注意してください。

✅ 次の課題
===
以下の `Check` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

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
    h5 {
    font-size: 16px;
    font-weight: 600
  }
  p span {
    font-size: 14px;
  }
  ul li span {
    font-size: 14px
  }
</style>
