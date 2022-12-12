---
slug: env-overview
id: 4zm4rievgnix
type: challenge
title: テスト環境の概要
teaser: このチャレンジでは、ACME Corp が
   *Let's Quiz!* アプリケーションをデプロイするために使用するさまざまな DevOps ツールを探ります。
注記:
- type: text
  コンテンツ: |-
    # チャレンジの概要
    このチャレンジでは、*Let's Quiz!* アプリケーションをデプロイメントするために ACME Corp が使用するツールを見ていきます。


    ![env_tools](../assets/img/env_tools.png)

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
- title: VS Code
  type: service
  hostname: controller
  path: /editor/?folder=/home/rhel/acme_corp
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
- title: コントローラー
  type: service
  hostname: controller
  port: 443
難易度: 基本
制限時間: 300
---
🔐 ログイン認証情報
===
すべてのログインで同じ認証情報が使用されます。

>ユーザー: student<p>
>パスワード: learn_ansible

👋 はじめに
===
#### 推定所要時間: *5 分*<p>
ACME Corp は、DevOps パイプラインでさまざまなツールを使用しています。これらの各ツールとその設定方法を見てみましょう。

☑️ タスク 1 - VS Code エディター
===


ACME Corp の開発者は `VS Code` IDE を使用しています。詳細を見ていきましょう。
* *VS Code* タブはデフォルトで開いています。

左ペインの *acme_corp* フォルダーの下に 2 つのフォルダーが表示されます。
  *  `app` フォルダーには *Let's Quiz!* アプリケーションコードが含まれています。
  *  `playbooks` フォルダーには、ラボで使用する Playbook が含まれています。


`playbooks` フォルダーには、*Let's Quiz!* アプリケーションのデプロイメントを自動化するために使用する Playbook が含まれています。

*  `playbooks` フォルダーをクリックします。

<!-- ![VSCode folders](../assets/img/vscode_folders.png) -->
<a href="#vscode_folders">
  <img alt="VSCode folders" src="../assets/img/vscode_folders.png" />
</a>

<a href="#" class="lightbox" id="vscode_folders">
  <img alt="VSCode folders" src="../assets/img/vscode_folders.png" />
</a>

>### **❗️注意**
>*ACME Corp* リポジトリーと *git* 設定はすでにセットアップされています。

☑️ タスク 2 - Gitea
===

ACME Corp はソースコード管理に *Gitea* を使用しており、*Let's Quiz!* アプリケーションコードリポジトリーが含まれています。

* ブラウザーウィンドウの上部にある *Gitea* タブをクリックします。
* 右上隅にある `Sign in` ボタンをクリックし、提供された認証情報を使用して *Gitea* にログインします。

<!-- ![Gitea signin](../assets/img/gitea_signin.png) -->

<a href="#gitea_signin">
  <img alt="Gitea signin" src="../assets/img/gitea_signin.png" />
</a>

<a href="#" class="lightbox" id="gitea_signin">
  <img alt="Gitea signin" src="../assets/img/gitea_signin.png" />
</a>

* 右側で、`Settings` をクリックしてから `Webhooks` をクリックします。

<!-- ![Gitea webhook](../assets/img/gitea_webhook.png) -->

<a href="#gitea_webhook">
  <img alt="Gitea webhook" src="../assets/img/gitea_webhook.png" />
</a>

<a href="#" class="lightbox" id="gitea_webhook">
  <img alt="Gitea webhook" src="../assets/img/gitea_webhook.png" />
</a>


*Gitea* には、新しいコードがリポジトリーにコミットされたときに Jenkins ジョブを開始するように設定された webhook があります。以下のチャレンジでは この webhook を使用します。



☑️ タスク 3 - Jenkins
===

ACME Corp は Jenkins を使用して、*Let's Quiz!* アプリケーションでいくつかの開発タスクを実行しています。

* ブラウザーウィンドウの上部にある *Jenkins* タブをクリックします。
* 右上隅にある `log in` ボタンをクリックし、提供された認証情報を使用して、*Jenkins* にログインします。

<!-- ![Jenkins login](../assets/img/jenkins_login.png) -->
<a href="#jenkins_login">
  <img alt="Jenkins login" src="../assets/img/jenkins_login.png" />
</a>

<a href="#" class="lightbox" id="jenkins_login">
  <img alt="Jenkins login" src="../assets/img/jenkins_login.png" />
</a>

`ACMECorp` Jenkins ジョブはデフォルトで読み込まれます。パイプラインは、基本的な開発タスクを実行します。これについては、次の演習で詳しく説明します。

<!-- ![ACMECorp status](../assets/img/jenkins_acme_landing.png) -->
<a href="#jenkins_acme_landing">
  <img alt="ACMECorp status" src="../assets/img/jenkins_acme_landing.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acme_landing">
  <img alt="ACMECorp status" src="../assets/img/jenkins_acme_landing.png" />
</a>

☑️ タスク 4 - コントローラー
===

ACME Corp のオペレーションでは、自動コントローラーを環境内で広く使用しています。

* 上部の *Controller* タブをクリックし、提供された認証情報を使用してログインします。
* 提供された認証情報を使用して `Log In` ボタンをクリックし、*controller* にログインします。

<!-- ![Controller login](../assets/img/controller_login.png) -->
<a href="#controller_login">
  <img alt="Controller login" src="../assets/img/controller_login.png" />
</a>

<a href="#" class="lightbox" id="controller_login">
  <img alt="Controller login" src="../assets/img/controller_login.png" />
</a>


* `Resources` で、`Templates` をクリックします。このメニューには、コントローラーで設定されている現在の *ジョブテンプレート* が表示されます。

<!-- ![ACMECorp JTs](../assets/img//controller_jt_list.png) -->
<a href="#controller_jt_list">
  <img alt="ACMECorp JTs" src="../assets/img//controller_jt_list.png" />
</a>

<a href="#" class="lightbox" id="controller_jt_list">
  <img alt="ACMECorp JTs" src="../assets/img//controller_jt_list.png" />
</a>

* 横にあるチェックボックスをクリックして、`DevOps Workflow` ジョブテンプレートを選択します。
* `DevOps Workflow` ジョブテンプレートの右側にある `Visualizer` ボタンをクリックします。

<!-- ![DevOps Workflow button](../assets/img/controller_devops_visualizer.png) -->
<a href="#controller_devops_visualizer">
  <img alt="DevOps Workflow button" src="../assets/img/controller_devops_visualizer.png" />
</a>

<a href="#" class="lightbox" id="controller_devops_visualizer">
  <img alt="DevOps Workflow button" src="../assets/img/controller_devops_visualizer.png" />
</a>

*DevOps Workflow* ジョブテンプレートは、複数のタスクを論理的で一貫したプロセスに統合します。このラボでは、これらのタスクについて詳しく見ていきます。

<!-- ![DevOps Workflow visual](../assets/img/controller_devops_visualizer_workflow.png) -->
<a href="#controller_devops_visualizer_workflow">
  <img alt="DevOps Workflow visual" src="../assets/img/controller_devops_visualizer_workflow.png" />
</a>

<a href="#" class="lightbox" id="controller_devops_visualizer_workflow">
  <img alt="DevOps Workflow visual" src="../assets/img/controller_devops_visualizer_workflow.png" />
</a>

>### **❗️注意**<p>
> 自動コントローラーは、DevOps ツールやワークフローをオーケストレーションするために、豊富な API、Workflow、Webhook などの機能を提供しています。<p>

✅ 次のチャレンジ
===
以下の `Next` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

NORMAL で問題が発生していますか ?
====
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
