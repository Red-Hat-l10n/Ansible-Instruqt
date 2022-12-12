---
slug: controller-approval
id: xwdgcvhu6tgk
type: challenge
title: コントローラーでのアプリケーションデプロイメントの承認
teaser: 最後に、新しいリリースをビルドするためのコントローラーのワークフローを承認し、Web サーバーを
  設定して、Let's Quiz! アプリケーションをデプロイします。
注記:
- type: text
  内容: |-
    # チャレンジの概要
    このチャレンジでは、コントローラーを使用して、*Let's Quiz!* アプリケーションを承認および設定し、実稼働環境にデプロイします。これを実現するために、自動コントローラーの Workflows ノードおよび Approval ノードを使用します。

    ![env_tools](../assets/img/slides_4_approve_deploy.png)

    <style type="text/css" rel="stylesheet">
    h1,h2{
      text-align: center;
    }
    p {
      text-align: center;
    }
    img {
      display: block;
      margin-left: auto;
      margin-right: auto;
      width: 80%;
    }
    </style>
タブ:
- title: Controller
  type: service
  hostname: controller
  port: 443
- title: Gitea
  type: service
  hostname: gitea
  path: /student/acme_corp
  port: 3000
- title: Jenkins
  type: service
  hostname: jenkins
  path: /job/ACMECorp/
  port: 8080
- title: Let's Quiz!
  type: service
  hostname: controller
  port: 8000
難易度: 中級
時間制限: 600
---
🔐 ログイン認証情報
===
すべてのログインで同じ認証情報が使用されます。

>ユーザー: student<p>
>パスワード: learn_ansible

👋 はじめに
===

#### 推定所要時間: _10 分_

前回のチャレンジでは、**home.html** ページを編集することで Jenkins パイプラインを開始しました。このチャレンジでは、自動コントローラーを使用して、_Let's Quiz!_ アプリケーションの承認とデプロイを行います。

>### **❗️ 注記**
> このチャレンジのチェックは、Jenkins パイプラインの完了時間に変動が生じる可能性があるため、数秒長くかかる場合があります。

☑️ タスク 1 - コントローラーで DevOps ワークフローを詳細に見る
===

ACME Corp のオペレーションは、`DevOps Workflow` と呼ばれる [コントローラーワークフロー](https://docs.ansible.com/automation-controller/4.2.0/html/userguide/workflows.html) を作成しました。このワークフローは、Web サーバーの設定、ACMECorp リポジトリーでのアプリケーションリリースの作成、そしてアプリケーションの実稼働環境へのデプロイを 1 つのプロセスにまとめたものです。

**_visualizer_ を使用して、DevOps Workflow のレイアウトを詳しく見てみましょう。**

* デフォルトで _Controller_ タブが開いているはずです。
* 必要な場合は、提供された認証情報を使用してログインしてください。
* `Resources` で、`Templates` をクリックします。このアクションは、コントローラーで設定された `DevOps Workflow` ジョブテンプレートを表示します。

<!-- ![ACMECorp JTs ](../assets/img//controller_jt_list.png) -->
<a href="#controller_jt_list">
  <img alt="Controller" src="../assets/img/controller_jt_list.png" />
</a>

<a href="#" class="lightbox" id="controller_jt_list">
  <img alt="Controller" src="../assets/img/controller_jt_list.png" />
</a>


* `DevOps Workflow` ジョブテンプレートの右側にある `visualizer` ボタンをクリックします。

<!-- ![DevOps Workflow button](../assets/img/controller_devops_visualizer.png) -->
<a href="#controller_devops_visualizer">
  <img alt="Controller" src="../assets/img/controller_devops_visualizer.png" />
</a>

<a href="#" class="lightbox" id="controller_devops_visualizer">
  <img alt="Controller" src="../assets/img/controller_devops_visualizer.png" />
</a>

`DevOps Workflow` ジョブテンプレートは、複数のタスクを論理的で一貫したプロセスに統合します。

<!-- ![DevOps Workflow visual](../assets/img/controller_devops_visualizer_workflow.png) -->
<a href="#controller_devops_visualizer_workflow">
  <img alt="Controller" src="../assets/img/controller_devops_visualizer_workflow.png" />
</a>

<a href="#" class="lightbox" id="controller_devops_visualizer_workflow">
  <img alt="Controller" src="../assets/img/controller_devops_visualizer_workflow.png" />
</a>

**`DevOps Workflow` ジョブテンプレートノードを詳細に見る**

* **Deploy to Prod?** \- このコントローラーの [承認ノード](https://docs.ansible.com/automation-controller/latest/html/userguide/workflow_templates.html#approval-nodes) により、意思決定者は、アプリケーションの実稼働環境へのデプロイを承認することができます。
* **Create App Release** \- 通常、開発者が実行するこの手順では、_ACMECorp_ パイプラインで生成された `tag_name` 変数を使用して、新しい _Let's Quiz!_ リリースを _Gitea_ に作成します。
* **Config Webservers** \- 通常、オペレーションが実行するこの手順では、_Let's Quiz!_ アプリケーションに必要な依存関係をインストールすることによって、Web サーバーを設定します。
* **Deploy ACME App** \- この手順では、アプリケーションの最新リリースをインストールし、実行します。
* **DevOps Workflow** を確認したら、右上隅にある X ボタンをクリックして _visualizer_ UI を終了します。

☑️ タスク 2 - コントローラーでの DevOps Workflow の承認
===

ACME Corp のオペレーションでは、`Deploy to Prod` と呼ばれるコントローラー [承認ノード](https://docs.ansible.com/automation-controller/latest/html/userguide/workflow_templates.html#approval-nodes) を `DevOps Workflow` ジョブテンプレートに追加しました。この手順により、ACME Corp の意思決定者は、_Let’s Quiz!_ の対象サーバーで十分な容量が利用可能であることを確認するなど、最終チェックを実行することができます。

現在、新しい _Let’s Quiz!_ アプリケーションはデプロイされていません。

**_Let's Quiz!_ アプリケーションの実稼働デプロイメントを承認します。**

* *Controller* タブが開いていない場合は、ブラウザーウィンドウの上部にある *Controller* タブをクリックします。
* 必要な場合は、提供された認証情報を使用してログインしてください。
* コントローラー UI の右上隅にある _notification_ アイコンをクリックすると、_Workflow Approval_ のインターフェイスが開きます。

<!-- ![Approval notification](../assets/img/controller_approval_notification.png) -->
<a href="#controller_approval_notification">
  <img alt="Controller" src="../assets/img/controller_approval_notification.png" />
</a>

<a href="#" class="lightbox" id="controller_approval_notification">
  <img alt="Controller" src="../assets/img/controller_approval_notification.png" />
</a>

_Workflow Approval_ インターフェイスは、承認されたユーザーが、自動化タスクを承認または拒否できる場所です。

* 左側の `Deploy to Prod?` の横の _checkbox_ をクリックします。
* *Workflow Approvals* UI の上部にある **Approve** ボタンをクリックします。

<!-- ![Approval workflow](../assets/img/controller_approve_workflow.png) -->
<a href="#controller_approve_workflow">
  <img alt="Controller" src="../assets/img/controller_approve_workflow.png" />
</a>

<a href="#" class="lightbox" id="controller_approve_workflow">
  <img alt="Controller" src="../assets/img/controller_approve_workflow.png" />
</a>

☑️ タスク 3 - DevOps Workflow の結果の表示
===

`DevOps Workflow` が承認されると、Web サーバーの設定、新しい _Let’s Quiz_ リリースの作成、実稼働環境へのデプロイを開始します。

**`DevOps Workflow` コントローラージョブ**

* _Controller_ タブで、`Views` の下にある `Jobs` をクリックします。
* `DevOps Workflow` ジョブをクリックします。

<!-- ![Jobs](../assets/img/controller_jobs_menu.png) -->
<a href="#controller_jobs_menu">
  <img alt="Controller" src="../assets/img/controller_jobs_menu.png" />
</a>

<a href="#" class="lightbox" id="controller_jobs_menu">
  <img alt="Controller" src="../assets/img/controller_jobs_menu.png" />
</a>

このアクションにより、`DevOps Workflow` _Output_ インターフェイスが開きます。緑色は、すべてのタスクが正常に完了したことを示しています。

また、`DevOps Workflow` _Output_ インターフェイスで、実行結果や詳細をさらに詳しく確認することもできます。

* `Create App Release` ノードをクリックします。

<!-- ![App release node](../assets/img/controller_app_release_node.png) -->
<a href="#controller_app_release_node">
  <img alt="Controller" src="../assets/img/controller_app_release_node.png" />
</a>

<a href="#" class="lightbox" id="controller_app_release_node">
  <img alt="Controller" src="../assets/img/controller_app_release_node.png" />
</a>

このアクションは、`Create App Release`  [コントローラージョブ](https://docs.ansible.com/automation-controller/latest/html/userguide/job_templates.html#view-completed-jobs) の詳細を表示します。

**`Create App Release` コントローラージョブを詳しく見てみましょう。**
* *Jenkins* ユーザーがビルドをトリガーしたことに留意してください。コントローラーは [RBAC](https://docs.ansible.com/automation-controller/latest/html/userguide/users.html) 機能を提供し、ACME Corp はワークフローの実行に必要な最低限の権限を持つ *Jenkins* ユーザーを作成しました。

<!-- ![App release user](../assets/img/controller_app_release_launched_by.png) -->
<a href="#controller_app_release_launched_by">
  <img alt="Controller" src="../assets/img/controller_app_release_launched_by.png" />
</a>

<a href="#" class="lightbox" id="controller_app_release_launched_by">
  <img alt="Controller" src="../assets/img/controller_app_release_launched_by.png" />
</a>

* _Variables_ セクションで、`tag_name` 変数が `Create App Release` ジョブテンプレートで正常に使用されたことに留意してください。

<!-- ![App release vars](../assets/img/controller_app_release_vars.png) -->
<a href="#controller_app_release_vars">
  <img alt="Controller" src="../assets/img/controller_app_release_vars.png" />
</a>

<a href="#" class="lightbox" id="controller_app_release_vars">
  <img alt="Controller" src="../assets/img/controller_app_release_vars.png" />
</a>

* 上記の `Details` タブの隣にある `Output` タブをクリックします。

`Output` インターフェイスには、`Create App Release` ジョブテンプレートの実行出力が表示されます。

<!-- ![App release output](../assets/img/controller_app_release_output.png) -->
<a href="#controller_app_release_output">
  <img alt="Controller" src="../assets/img/controller_app_release_output.png" />
</a>

<a href="#" class="lightbox" id="controller_app_release_output">
  <img alt="Controller" src="../assets/img/controller_app_release_output.png" />
</a>


☑️ タスク 4 - 新しい Let’s Quiz! リリース
===

`Create App Release` ジョブテンプレートは、`acme_corp` _Gitea_ リポジトリーに新しいリリースを作成しました。

**最新のリリースを見てみましょう。**

* ブラウザーウィンドウの上部にある _Gitea_ タブをクリックします。
* 必要であれば、提供された認証情報を使用して _Gitea_ にログインしてください。
* トップメニューの `Releases` タブをクリックします。

<!-- ![Gitea release](../assets/img/gitea_new_release.png) -->
<a href="#gitea_new_release">
  <img alt="Gitea" src="../assets/img/gitea_new_release.png" />
</a>

<a href="#" class="lightbox" id="gitea_new_release">
  <img alt="Gitea" src="../assets/img/gitea_new_release.png" />
</a>


* 新しいリリースでは、ACME Corp のパイプラインで生成された `tag_name` 変数の値が使用されていることに留意してください。

ACME Corp のオペレーションは、関連する `TAR.GZ` ファイルを使用して、_Let's Quiz!_ アプリケーションを実稼働環境にデプロイしました。

☑️ タスク 5 - ACMECorp パイプラインの確認
===

**ACMECorp パイプラインのステータスを確認しましょう。**
* ブラウザーウィンドウの上部にある _Jenkins_ タブをクリックします。
* 必要であれば、提供された認証情報を使用して _Jenkins_ にログインしてください。

<!-- ![Gitea release](../assets/img/jenkins_acme_success.png) -->
<a href="#jenkins_acme_success">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_success.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acme_success">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_success.png" />
</a>


*ACMECorp パイプライン* は、`DevOps Workflow` ジョブテンプレートがすべてのタスクを完了すると、正常に完了したことを示す _green_ のステータスを表示します。

☑️ タスク 7 - Let’s Quiz! ホームページへのアクセス
===

最後になりましたが、_Let's Quiz!_ アプリケーションの実稼働デプロイメントは正常に実行されたはずです。

**ホームページを確認して、変更点を見てみましょう。**
* ブラウザーのウィンドウ上部にある Let's Quiz! タブをクリックします。
* ホームページには、前のチャレンジで追加した更新されたテキストがあることに留意してください。

<!-- ![App working](../assets/img/app_page_updated.png) -->
<a href="#app_page_updated">
  <img alt="App" src="../assets/img/app_page_updated.png" />
</a>

<a href="#" class="lightbox" id="app_page_updated">
  <img alt="App" src="../assets/img/app_page_updated.png" />
</a>

🎉 お疲れさまでした。
===

**チャレンジの完了、おめでとうございます!**

[自動コントローラー](https://www.ansible.com/products/controller) は、既存のテクノロジーと統合し、企業全体の DevOps プラクティスを向上させるための広範な API、Webhook、Workflow、および他の多くのソリューションを提供します。

以下のような、**[Ansible Automation Platform](https://www.redhat.com/en/technologies/management/ansible#:~:text=Ansible%20Automation%20Platform%20provides%20an,to%20security%20and%20network%20teams) が提供するエンタープライズ機能をいくつか説明しました。**
* [ワークフロージョブテンプレート](https://docs.ansible.com/automation-controller/latest/html/userguide/workflow_templates.html) を使用すると、より複雑なユースケースを解決するために、自動化の小さな部分を論理的に連結して再利用することができます。
* 自動コントローラーは、現在の DevOps プラクティスを増強、統合、向上させ、複数の IT ドメインと環境にまたがる広範な [API](https://docs.ansible.com/automation-controller/latest/html/controllerapi/index.html) を提供します。

**さらに、Ansible Automation Platform は、現在の DevOps プラクティスを強化するための複数の機能を提供します。**
* [Ansible Content Collections](https://www.ansible.com/products/content-collections) は、ビルド済み、テスト済み、認定済みの自動化コンテンツを提供して、自動化への参入障壁を下げ、ツール統合に関連する運用上のオーバーヘッドを削減します。
* [自動コントローラー webhooks](https://docs.ansible.com/automation-controller/4.2.0/html/userguide/webhooks.html) は、Ansible Automation Platform を現在の CI/CD ツールと統合するための追加オプションを提供します。


✅次の場所
===

自動化への取り組みを始めたばかりの方でも、経験豊富なベテランの方でも、自動化の知識を深めるためのさまざまなリソースを利用できます。

* [自分のペースで進められる演習](https://www.redhat.com/en/engage/redhat-ansible-automation-202108061218) - 自分のペースで進められるすべてのラボをご覧ください。
* [トライアルサブスクリプション](http://red.ht/try_ansible) - お使いの環境にインストールする準備はできていますか?Ansible Automation Platform のすべてのコンポーネントに無制限にアクセスするには、トライアルサブスクリプションを取得してください。
* [Red Hat Ansible Automation Platform の YouTube チャンネルへのサブスクライブ。](https://www.youtube.com/ansibleautomation)

✅ 次のチャレンジ - プレイグラウンド
===

次のチャレンジでは、残りの時間を使って操作を確認したり、実践したりします。ぜひ、お試しください。

タスクが完了したら、以下の `Check` ボタンを押して次のチャレンジに移動します。

🐛 問題が発生しましたか?
====
ワークフロー全体を再起動する必要がある場合は、自動コントローラーで `Restart DevOps Workflow` ジョブテンプレートを実行します。

問題が発生した場合や気になる点がある場合は、[チケットを作成](https://github.com/ansible/instruqt/issues/new?labels=devops-controller&title=New+DevOps+with+automation+controller+issue+issue:+incident-creation&assignees=craig-br) してください。

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
