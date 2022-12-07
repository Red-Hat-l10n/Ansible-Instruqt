---
slug: mesh-instance-groups
id: 1rqwfn5u2dx1
type: challenge
title: Automation Mesh およびインスタンスグループ
teaser: 新規インスタンスグループの作成およびローカルおよびリモート実行のメッシュワーカーノードの割り当て
  
注記:
- type: text
  コンテンツ: "# \\U0001F44B インスタンスおよびインスタンスグループ\\n\\n![node_overview](../assets/img/instance_groups_main.png)\\n\\nIn
    この課題では、ACME Corp Raleigh のコントローラーインスタンスグループを作成します。
    Johannesburg リージョンおよびAutomation Mesh ワーカーノードを関連付けます。\\n\\n<style
    type="text/css" rel="stylesheet">\\nh1,h2{\\n  text-align: center;\\n}\\np {¨\\n
    \\ text-align: center;\\n}\\nimg {\\n  display: block;\\n  margin-left: auto;\\n  margin-right:
    auto;\\n  height: 60%;\\n\\n}\\n</style>"
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

最後のチャレンジでは、異なるメッシュノードタイプ、インスタンスおよびインスタンスグループ、および **トポロジービューアー** について説明しました。

この課題では、ACME Corp が Raleigh および Johannesburg の新しいインスタンスグループを作成し、これらのグループにインスタンスを割り当てるのに役立ちます。

>**❗️注意**
>
> * ブラウザーの左上にある _Controller_ タブで、すべてのタスクを実行します。
> * 必要な場合は、提供された認証情報を使用してAutomation Controller にログインします。
> * イメージをクリックして詳しく見ると、イメージを拡張することができます。

☑️ タスク: インスタンスグループの作成および設定
===

>ℹ️ [インスタンスグループ](https://docs.ansible.com/automation-controller/latest/html/administration/containers_instance_groups.html) は、メッシュノードを論理的にグループ化して、_インベントリー_、_組織_ およびジョブ _テンプレート_ などのさまざまなコントローラーオブジェクトに割り当て可能です。

ACME Corp は、最も近いメッシュワーカーノードが自動化を実行することを確認するために、正しいインスタンスを Raleigh および Johannesburg の場所に関連付ける必要があります。

>**❗️注意**\
>この課題では、インスタンスグループを作成し、インスタンスを関連付けます。次の課題では、インスタンスグループを適切なコントローラー _インベントリー_ に割り当て、_ジョブテンプレート_ を実行することで最後のステップを完了します。

##### ☑️ Raleigh データセンター用の新しいインスタンスグループを作成しましょう。

* **Administration** セクションのサイドナビゲーションで、**Instance Groups** をクリックします。
* **Add** をクリックし、**Add instance group** を選択します。
* 新しいインスタンスグループを作成して名前を付けます。

  ```text
  Raleigh data center
  ```

* **Save** をクリックします｡

<a href="#mesh_raleigh_ig_create">
  <img alt="mesh_raleigh_ig_create" src="../assets/img/mesh_raleigh_ig_create.png" />
</a>

<a href="#" class="lightbox" id="mesh_raleigh_ig_create">
  <img alt="ACME メッシュ" src="../assets/img/mesh_raleigh_ig_create.png" />
</a>

##### 次に、`raleigh-controller` インスタンスを `Raleigh データセンター` インスタンスグループに関連付けます。

* トップメニューの **Instances** をクリックします。
* **Associate** をクリックします。
* `raleigh-controller` インスタンスを選択し、**Save** をクリックします。

<a href="#mesh_raleigh_associate_instance">
  <img alt="mesh_raleigh_associate_instance" src="../assets/img/mesh_raleigh_associate_instance.png" />
</a>

<a href="#" class="lightbox" id="mesh_raleigh_associate_instance">
  <img alt="mesh_raleigh_associate_instance" src="../assets/img/mesh_raleigh_associate_instance.png" />
</a>

##### ✏️ Johannesburg データセンター用の新しいインスタンスグループを作成しましょう。

* **Administration** セクションのサイドナビゲーションで、**Instance Groups** をクリックします。
* **Add** をクリックし、**Add instance group** を選択します。
* 新しいインスタンスグループを作成して名前を付けます。

  ```text
  Johannesburg data center
  ```

* **Save** をクリックします｡

<a href="#mesh_jhb_ig_create">
  <img alt="mesh_jhb_ig_create" src="../assets/img/mesh_jhb_ig_create.png" />
</a>

<a href="#" class="lightbox" id="mesh_jhb_ig_create">
  <img alt="ACME メッシュ" src="../assets/img/mesh_jhb_ig_create.png" />
</a>

##### 次に、`jhb-exec` インスタンスを `Johannesburg データセンター` インスタンスグループに関連付けます。

* トップメニューの **Instances** をクリックします。
* **Associate** をクリックします。
* `jhb-exec` インスタンスを選択し、**Save** をクリックします。

<a href="#jhb_exec_associate">
  <img alt="jhb_exec_associate" src="../assets/img/jhb_exec_associate.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_associate">
  <img alt="jhb_exec_associate" src="../assets/img/jhb_exec_associate.png" />
</a>

☑️ タスク：インスタンスのヘルスチェック
===

Automation Mesh は、メッシュノードでヘルスチェックを実行して、最適なルートおよび自動化ジョブの割り当てを決定します。

##### Johannesburg の `jhb-exec` でヘルスチェックを実行しましょう。

* **Administration** セクションのサイドナビゲーションで、**Topology View** をクリックします。
* トポロジーの `jhb-exec` ノードをクリックします。
* 右上にある *Details* セクションで `jhb-exec` リンクをクリックします。

<a href="#jhb_exec_topology_click">
  <img alt="jhb_exec_topology_click" src="../assets/img/jhb_exec_topology_click.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_topology_click">
  <img alt="jhb_exec_topology_click" src="../assets/img/jhb_exec_topology_click.png" />
</a>

* **Health Check** をクリックします。

<a href="#jhb_exec_health_check">
  <img alt="jhb_exec_health_check" src="../assets/img/jhb_exec_health_check.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_topology_click">
  <img alt="jhb_exec_health_check" src="../assets/img/jhb_exec_health_check.png" />
</a>

*Last Health Check* の日時に注意してください。

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
  p span {
    font-size: 14px;
  }
  ul li span {
    font-size: 14px
  }
</style>
