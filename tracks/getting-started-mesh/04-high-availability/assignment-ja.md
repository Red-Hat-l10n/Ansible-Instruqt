---
slug: high-availability
id: 25lcerewvn3e
type: challenge
title: メッシュを使用した回復性の高い自動化
teaser: Automation Mesh には、ワーカーノード全体で柔軟な設計オプションと、
  ネイティブの耐障害性が搭載されています。
注記:
- type: text
  コンテンツ: "# \\U0001F631 ACME Corp ネットワークの停止\\n\\n![env_tools](../assets/img/disconnected.png)\\n\\n
    Raleigh と Johannesburg 間のネットワークが新たに停止され、
    Johannesburg リモートオフィスで自動化を実行できなくなっています。\\n\\n今回の課題では、
    Dublin のホップノードを有効化して、そのホップノードを使って、
    Dublin と Johannesburg の間にある既存のバックアップネットワークリンクで自動化トラフィックをルートします。\\n\\n<style type="text/css"
    rel="stylesheet">\\nh1,h2{\\n  text-align: center;\\n}\\np {\\n  text-align: center;\\n}\\nimg
    {\\n  display: block;\\n  margin-left: auto;\\n  margin-right: auto;\\n  width: 80%;\\n}\\n</style>"
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

ACME Corp では、Raleigh データセンターと Johannesburg リモートオフィスの間のネットワークが停止しています。Dublin 経由で Raleigh と Johannesburg の間にバックアップリンクが存在します。

<a href="#disconnected">
  <img alt="オフラインインストール" src="../assets/img/disconnected.png" />
</a>

<a href="#" class="lightbox" id="disconnected">
  <img alt="オフラインインストール" src="../assets/img/disconnected.png" />
</a>

この課題では、Dublin のホップノードを使用して Raleigh の Automation Controller を Johannesburg リモートオフィスに接続します。

>**❗️注意**
>
>* ブラウザーの左上にある _Controller_ タブで、すべてのタスクを実行します。
>* 必要な場合は、提供された認証情報を使用してAutomation Controller にログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。
>* 今回の課題のタスクチェックには、数秒かかる場合があります。

☑️ タスク: インスタンスのヘルスチェック実行
===

Automation Mesh はワーカーノードで定期的なヘルスチェックを実行します。これらのヘルスチェックは、コントローラーの WebUI または API 経由でトリガーできます。

>**❗️注意**
>
>* コントローラービューによっては、このデモ環境でさまざまな正常性の *ステータス* 情報を表示する同じメッシュワーカーノードが表示される場合があります。
>* サポート対象のインストール設計では、これは発生しません。
>* サポートされているパターンの詳細は、[official documentation](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.0-ea/html/red_hat_ansible_automation_platform_installation_guide/index) を参照してください。



##### ✏️ Johannesburg 実行ノードでヘルスチェックを実行しましょう。

* **Administration** セクションのサイドナビゲーションで、**Topology View** をクリックします。

<a href="#jhb_exec_topology_unhealthy">
  <img alt="jhb_exec_topology_unhealthy" src="../assets/img/jhb_exec_topology_unhealthy.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_topology_unhealthy">
  <img alt="jhb_exec_topology_unhealthy" src="../assets/img/jhb_exec_topology_unhealthy.png" />
</a>

`jhb-exec` に _Error_ ステータスが表示されることに注意してください。

* トポロジーの `jhb-exec` ノードをクリックします。
* ウィンドウの右上にある *Details* で、`jhb-exec` リンクをクリックします。これにより、新しいウィンドウが開きます。
* **Health Check** ボタンをクリックして、_Error_ ステータスを確認します。完了するまでに数秒かかります。

<a href="#jhb_exec_unhealthy">
  <img alt="jhb_exec_unhealthy" src="../assets/img/jhb_exec_unhealthy.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_unhealthy">
  <img alt="jhb_exec_unhealthy" src="../assets/img/jhb_exec_unhealthy.png" />
</a>

*Errors* ボックスのメッセージをメモします。`jhb-exec` ノードにははAutomation Controller から到達できません。

☑️ タスク - Mesh ルート情報ジョブテンプレートの実行
===

`Mesh route info` ジョブテンプレートは、Johannesburg で自動化ジョブの実行に使用するパスメッシュを表示します。

##### `Mesh route info` ジョブテンプレートを使用して、`jhb-exec` インスタンスに到達できないことを確認します。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Mesh route info` ジョブテンプレートの横にある <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックして、これを起動します。

<a href="#route_info_launch">
  <img alt="route_info_launch" src="../assets/img/route_info_launch.png" />
</a>

<a href="#" class="lightbox" id="route_info_launch">
  <img alt="route_info_launch" src="../assets/img/route_info_launch.png" />
</a>

* 新しいウィンドウに、インベントリーの選択を求めるプロンプトが表示されます。デフォルトで `Raleigh DC` に選択されている項目をそのまま使用します。
* **Next** をクリックし、**Launch** をクリックします。

<a href="#route_info_raleigh_fail">
  <img alt="route_info_raleigh_fail" src="../assets/img/route_info_raleigh_fail.png" />
</a>

<a href="#" class="lightbox" id="route_info_raleigh_fail">
  <img alt="route_info_raleigh_fail" src="../assets/img/route_info_raleigh_fail.png" />
</a>

`Mesh route info` ジョブテンプレートの出力に注意してください。

```text
Error no route to node from raleigh-controller
```

☑️ タスク - ダブリンホップノードの設定
===

ACME Corp では、`dublin-hop` ホップノードを有効にして、Raleigh と Johannesburg の間で自動化トラフィックをルーティングする必要があります。`Setup Dublin hop node` ジョブテンプレートと、Automation Controller に新しい `Dublin DC` インベントリーを作成し、設定を実行しました。

>**❗️注意**
>
>`Setup Dublin hop node` ジョブテンプレートは、Automation Mesh の回復性について簡単に例示しています。サポートされているアーキテクチャーおよびベストプラクティスについては、[official documentation](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.2)を参照してください。

##### ✏️ では `Setup Dublin hop node` ジョブテンプレートを実行し、`dublin-hop` ノードを有効にしてみましょう。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Setup Dublin hop ノード` ジョブテンプレートの横にある <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックして、これを起動します。

<a href="#setup_dublin_inv">
  <img alt="setup_dublin_inv" src="../assets/img/setup_dublin_inv.png" />
</a>

<a href="#" class="lightbox" id="setup_dublin_inv">
  <img alt="setup_dublin_inv" src="../assets/img/setup_dublin_inv.png" />
</a>

* 新しいウィンドウに、インベントリーの選択を求めるプロンプトが表示されます。デフォルトで `Dublin DC` に選択されている項目をそのまま使用します。
* **Next** をクリックし、**Launch** をクリックします。

<a href="#setup_dublin_output">
  <img alt="setup_dublin_output" src="../assets/img/setup_dublin_output.png" />
</a>

<a href="#" class="lightbox" id="setup_dublin_output">
  <img alt="setup_dublin_output" src="../assets/img/setup_dublin_output.png" />
</a>

ジョブテンプレートには、`dublin-hop` の現在のステータスが表示されます。Automation Mesh は、ルーティングテーブルに `dublin-hop` を動的に追加することに注意してください。

☑️ タスク - Johannesburg が到達可能であることの確認
===

>☑️ Automation Mesh は、Dublin hop、Johannesburg 実行、および Raleigh ハイブリッドノードを動的にピアリングし、メッシュルーティングテーブルを更新しました。

##### ✏️ Johannesburg データセンターへの新しいルートを確認しましょう。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Mesh route info` ジョブテンプレートの横にある <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックして、これを起動します。
* 新しいウィンドウに、インベントリーの選択を求めるプロンプトが表示されます。デフォルトで `Raleigh DC` に選択されている項目をそのまま使用します。
* **Next** をクリックし、**Launch** をクリックします。

<a href="#route_info_raleigh_hop">
  <img alt="route_info_raleigh_hop" src="../assets/img/route_info_raleigh_hop.png" />
</a>

<a href="#" class="lightbox" id="route_info_raleigh_hop">
  <img alt="route_info_raleigh_hop" src="../assets/img/route_info_raleigh_hop.png" />
</a>

`dublin-hop` は `jhb-exec` に到達するために使用されます。

☑️ タスク - jhb-exec の正常性ステータスの確認
===

>**❗️注意**
>
>* コントローラービューによっては、このデモ環境でさまざまな正常性の *ステータス* 情報を表示する同じメッシュワーカーノードが表示される場合があります。
>* サポート対象のインストール設計では、これは発生しません。
>* サポートされているパターンの詳細は、[official documentation](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.0-ea/html/red_hat_ansible_automation_platform_installation_guide/index) を参照してください。

**`jhb-exec` が正常な状態であることを確認しましょう。**

* **Administration** セクションのサイドナビゲーションで、**Topology View** をクリックします。
* トポロジーの `jhb-exec` ノードをクリックします。
* 右上にある *Details* セクションで `jhb-exec` リンクをクリックします。
* **Health Check** ボタンをクリックします。完了するまでに数秒かかります。

<a href="#jhb_exec_healthy_check">
  <img alt="jhb_exec_healthy_check" src="../assets/img/jhb_exec_healthy_check.png" />
</a>

<a href="#" class="lightbox" id="jhb_exec_healthy_check">
  <img alt="jhb_exec_healthy_check" src="../assets/img/jhb_exec_healthy_check.png" />
</a>

`jhb-exec` が正常なステータスを表示するようになりました。

Johannesburg リモートオフィスでの自動化の実行
===

##### Johannesburg で `Debug info` ジョブテンプレートを使用して、Johannesburg で自動化を実行できることを確認しましょう。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* Actions 列の <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックして、ジョブテンプレートを起動します。
* `Johannesburg DC` インベントリーを選択します。
* **Next** をクリックし、**Launch** をクリックします。

<a href="#debug_info_jhb_output">
  <img alt="debug_info_jhb_output" src="../assets/img/debug_info_jhb_output.png" />
</a>

<a href="#" class="lightbox" id="debug_info_jhb_output">
  <img alt="debug_info_jhb_output" src="../assets/img/debug_info_jhb_output.png" />
</a>

`Debug info` ジョブテンプレートは正常に実行されました !

🎉 お疲れさまでした。
===

**ラボを完了しました!**

このラボでは、[automation mesh](https://www.ansible.com/products/automation-mesh)の機能をいくつか説明しました。ただし、それ以外にも多くのサービスが提供されます。

**簡素化された操作 -** ジャンプホストや SSH プロキシーなどの補助ツールの依存関係を削除します。

**柔軟な設計オプション** \- 単一サイトのデプロイメントから、世界全体のプラットフォームのインストールまで対応できます。

**スケーリングの確実性**: ネイティブのフォールトトレランスおよび冗長性、接続の中断やネットワークのレイテンシーに対する回復性があるホップノードなどの新機能。

**安全なスケーリング** Transport Layer Security (TLS) 暗号化および、コントローラー経由での一言管理で [RBAC (ロールベースアクセス制御)](https://docs.ansible.com/automation-controller/latest/html/userguide/security.html#role-based-access-controls) などの機能の活用。

✅次の場所
===
自動化への取り組みを始めたばかりの方でも、経験豊富なベテランの方でも、自動化の知識を深めるためのさまざまなリソースを利用できます。

* [自分のペースで進められる演習](https://www.redhat.com/en/engage/redhat-ansible-automation-202108061218) - 自分のペースで進められるラボをすべてご覧ください
* [トライアルサブスクリプション](http://red.ht/try_ansible) - お使いの環境にインストールする準備はできていますか?Ansible Automation Platform のすべてのコンポーネントに無制限にアクセスするには、トライアルサブスクリプションを取得してください。
* [Red Hat Ansible Automation Platform の YouTube チャンネルにサブスクライブします。](https://www.youtube.com/ansibleautomation)

✅ 次の課題 - プレイグラウンド
===

次の課題は、残りの時間を使って操作の確認や実践をする場所です。ぜひ、お試しください。\
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
    /* max-height: 100% */
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
