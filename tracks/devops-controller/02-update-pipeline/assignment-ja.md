---
slug: update-pipeline
id: t2481h50besa
type: challenge
title: ACME Corp のパイプラインを設定する
teaser: 自動コントローラーを使用して ACME Corp のパイプラインを設定し、統合します。
注記:
- type: text
  内容: |-
    # チャレンジの概要
    このチャレンジでは、API を使用して Jenkins を自動コントローラーに統合します。


    ![env_tools](../assets/img/slides_2_controller_api.png)

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
- title: Jenkins
  type: service
  hostname: jenkins
  path: /job/ACMECorp/
  port: 8080
- title: コントローラー
  type: service
  hostname: controller
  port: 443
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
#### 推定所要時間: _10 分_<p>

ACME Corp では、デプロイメント用にオペレーションにコードを手動で渡す前に、_Jenkins_ を使用して基本的な開発タスクとチェックを実行しています。

このラボでは、[ジョブテンプレート](https://docs.ansible.com/automation-controller/latest/html/userguide/job_templates.html) を使用して、Jenkins を _automation controller_ に統合するためのパイプラインを編集します。


>### **❗️ 注記**
>心配することはありません。このラボでは、Jenkins パイプラインのコーディングは行いませんので、詳細をすべて理解する必要はありません。

☑️ タスク 1 - ACME Corp パイプライン
===
ACMECorp パイプラインの手順を見てみましょう。

* _Jenkins_ タブはデフォルトで開いています。
* まだログインしていない場合は、提供された認証情報を使用してログインしてください。
* デフォルトのランディングページは `ACME Corp` パイプラインです。

<!-- ![ACMECorp Pipeline](../assets/img/jenkins_acmecorp_job.png) -->
<a href="#jenkins_acmecorp_job">
  <img alt="ACMECorp Pipeline" src="../assets/img/jenkins_acmecorp_job.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acmecorp_job">
  <img alt="ACMECorp Pipeline" src="../assets/img/jenkins_acmecorp_job.png" />
</a>


* Jenkins UI ウィンドウの左側で、`Configure` をクリックします。

<!-- ![ACMECorp Configure ](../assets/img/jenkins_acmecorp_configure.png) -->
<a href="#jenkins_acmecorp_configure">
  <img alt="ACMECorp Pipeline" src="../assets/img/jenkins_acmecorp_configure.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acmecorp_configure">
  <img alt="ACMECorp Pipeline" src="../assets/img/jenkins_acmecorp_configure.png" />
</a>

* _groovy_ コードを含む *Pipeline* セクションに到達するまで、ページの下部までスクロールします。

<!-- ![ACMECorp Job](../assets/img/jenkins_acme_initial_pipe.png) -->
<a href="#jenkins_acme_initial_pipe">
  <img alt="ACMECorp Job" src="../assets/img/jenkins_acme_initial_pipe.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acme_initial_pipe">
  <img alt="ACMECorp Job" src="../assets/img/jenkins_acme_initial_pipe.png" />
</a>

ACME Corp の開発者は、パイプラインに以下の手順を追加しました。

* **SCM Get Code** - _GItea_ リポジトリーから最新の _Let's Quiz!_ アプリケーションコードをプルします。
* **パッケージのインストール** \- アプリケーションのテストに必要なパッケージをインストールします。
* **静的コードチェック** \- 静的コード解析を実行します。
* **ビルドとタグ** - _Let's Quiz!_ アプリケーションのバージョンをインクリメントし、git タグを作成します。この新しいタグ番号は、次の手順で役に立つことがわかります。

☑️ タスク 2 - コントローラーと Jenkins の統合
===

ACME Corp のオペレーションでは、Ansible Automation Platform を広く使用しており、自動化をパイプラインに統合したいと考えています。この統合により、実稼働環境でのデプロイメントに一貫性を持たせることができます。

`Configure Jenkins Job` コントローラージョブテンプレートは、コントローラーのワークフローを開始するためにコントローラーの API を呼び出す手順を現在のパイプラインに追加します。

`Configure Jenkins Job` ジョブテンプレートを実行します。

* ブラウザーウィンドウの上部にある *Controller* タブをクリックします。
* まだログインしていない場合は、提供された認証情報を使用してログインしてください。
* `Resources` で、`Templates` をクリックします。このアクションは、コントローラーで設定されている現在の _Job Templates_ を表示します。
* 右側にある <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> のアイコンをクリックして、`Configure Jenkins Job` を実行します。

<!-- ![Controller Jenkins](../assets/img/controller_jenkins_jt.png) -->
<a href="#controller_jenkins_jt">
  <img alt="Controller Jenkins"" src="../assets/img/controller_jenkins_jt.png" />
</a>

<a href="#" class="lightbox" id="controller_jenkins_jt">
  <img alt="Controller Jenkins" src="../assets/img/controller_jenkins_jt.png" />
</a>

_Job Output_ ウィンドウでは、現在の ACMECorp パイプラインを正常に *変更* したことが確認できます。

<!-- ![JT output](../assets/img/controller_jt_jenkins_output.png) -->
<a href="#controller_jt_jenkins_output">
  <img alt="JT output" src="../assets/img/controller_jt_jenkins_output.png" />
</a>

<a href="#" class="lightbox" id="controller_jt_jenkins_output">
  <img alt="JT output" src="../assets/img/controller_jt_jenkins_output.png" />
</a>


☑️ タスク 3 - 更新された ACMECorp パイプライン
===

**次に、更新された Jenkins のパイプラインを見てみましょう。**

* ブラウザーウィンドウの上部にある _Jenkins_ タブをクリックします。
* トップメニューの `ACME Corp` をクリックしてから、`Configure` をクリックします。このアクションは、Jenkins UI を最新の変更内容で再読み込みします。
* パイプラインセクションまでスクロールダウンします。

パイプラインのコードに、新しい `Controller - DevOps` ステージが表示されます。

<!-- ![Pipeline step](../assets/img/jenkins_acme_plugin.png) -->
<a href="#jenkins_acme_plugin">
  <img alt="Pipeline step" src="../assets/img/jenkins_acme_plugin.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acme_plugin">
  <img alt="Pipeline step" src="../assets/img/jenkins_acme_plugin.png" />
</a>



> **❗️ 注記**<p>
>[Ansible Tower Jenkins プラグイン](https://plugins.jenkins.io/ansible-tower/) はコミュニティー主導で、このラボではデモ目的にのみ使用されます。
>
>プラグインは引き続き _Tower_ を参照していますが、このラボタスクのコントローラー API を正常に使用しています。


[Ansible Tower Jenkins プラグイン](https://plugins.jenkins.io/ansible-tower/) は、ジョブテンプレートを実行するために自動コントローラー API を使用します。設定を見てみましょう。

Jenkins で設定された自動コントローラーの名前 - `ACME Corp controller `
```groovy
towerServer: 'ACME Corp controller',
```
呼び出すジョブテンプレートのタイプ - `workflow`
```groovy
templateType: 'workflow',
```
Workflow Job Template の名前 - `DevOps Workflow`
```groovy
jobTemplate: 'DevOps Workflow',
```

コントローラー API は、API 呼び出しに余分な変数を渡すなど、複数のパラメーターを受け入れます。
```groovy
extraVars: '''---
pkg_version: $pkgVersion
tag_name: $newPkgVersion
'''
```
ACME Corp は、前の Jenkins の手順で作成された `$newPkgVersion` 変数を使用し、これを `tag_name` 変数としてコントローラーに渡します。この情報は、アプリケーションを正常にデプロイするために不可欠なものです。

✅ 次のチャレンジ
===
以下の `Check` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

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
