---
slug: install-edge-app
id: inoxr4coboga
type: challenge
title: 産業用エッジアプリケーションのインストール
teaser: このチャレンジでは、Ignition アプリケーションを Dublin ファクトリーにインストールします。
注記:
- type: text
  コンテンツ: "# 最初のミッション: アプリケーションをダブリン工場 HMI \\U0001F4F2 に一貫したスケーラブルな方法でデプロイ。
    \\n##### あなたはローリーを拠点としており、
    プリケーションをリモートで展開するタスクが課せられています｡\\n##### あなたは経験豊富なベテランなので \\U0001F94B
    本番前にアプリケーションのデプロイをテストし、コンテナー化したイメージ
    を準備しました｡\\U0001F947.\\n##### あなたのミッションは、
    ダブリン工場の HMI デバイスに工場制御アプリケーションを展開することです。\\U0001F4F2.\\n#####
    Start ボタンをクリックして受け入れます｡\\n\\n<center><img src="https://github.com/dafmendo/pictures_for_github/blob/a00524b755041463dcfe6b4860cd273e1c9c195c/industrialapp-deploy.png?raw=true"></center>\\n\\n\\n<style
    type="text/css" rel="stylesheet">\\nh1,h2{\\n  text-align: center;\\n}\\np {\\n
    \\ text-align: center;\\n}\\nimg {\\n  display: block;\\n  margin-left: auto;\\n  margin-right:
    auto;\\n  height: 60%;\\n\\n}\\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: controller-edge-lab
  port: 443
- title: Dublin アプリケーション
  type: service
  hostname: dublin-edge-lab
  path: /web/login
  port: 8088
  new_window: true
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

### 最初のミッション: 一貫したスケーラブルな方法でアプリケーションをダブリンの工場にデプロイする
Dublin 実行ノードを介して、産業用アプリケーションを Dublin factory HMI デバイスにデプロイします。
<a href="#dublin-deployment">
  <img alt="Dublin でのエッジアプリケーションのデプロイ" src="../assets/img/dublin-deployment.png" />
</a>

<a href="#" class="lightbox" id="dublin-deployment">
  <img alt="Dublin でのエッジアプリケーションのデプロイ" src="../assets/img/dublin-deployment.png" />
</a>

##### ⏰ 推定所要時間: *10 分*

>**❗️注意**
>
>* 必要な場合は、_Controller_ タブから提供された認証情報を使用して自動化コントローラーにログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。
>* 以下は、この例で使用されている Playbook への [リンク](https://github.com/craig-br/instruqt-track-content/blob/65e9c23585f22e0c725108c1277a4c524bf58513/getting-started-edge-lab/playbooks/deploy_application.yml) です。

☑️ 最初のタスク - エッジアプリケーションジョブテンプレートのデプロイ
===

>ℹ️[ジョブテンプレート](https://docs.ansible.com/automation-controller/latest/html/userguide/job_templates.html) は、同じジョブを何度も実行するのに役立ち、Ansible ジョブを実行するための定義とパラメーターのセットを設定します。

##### ✏️ **automation controller** で*Deploy edge application* ジョブテンプレートをデプロイメントするを参照してください。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Deploy edge application` ドロップダウン矢印をクリックします。

<a href="#deploy_app_template">
  <img alt="エッジアプリケーションをデプロイする" src="../assets/img/deploy_app_template.png" />
</a>

<a href="#" class="lightbox" id="deploy_app_template">
  <img alt="エッジアプリケーションをデプロイする" src="../assets/img/deploy_app_template.png" />
</a>

`Deploy edge application` ジョブテンプレートは、デフォルトで *Dublin region* インベントリーを使用します。これは、`Dublin instance group` を使用します。また、`Dublin nstance group` は、ローカルの `dublin-edge-lab` 実行ノードを使用して、すべての自動化ジョブを実行します。

<a href="#deploy_app_template_dublin">
  <img alt="エッジアプリケーションインベントリーのデプロイ" src="../assets/img/deploy_app_template_dublin.png" />
</a>

<a href="#" class="lightbox" id="deploy_app_template_dublin">
  <img alt="エッジアプリケーションインベントリーのデプロイ" src="../assets/img/deploy_app_template_dublin.png" />
</a>

##### ✏️ *Deploy edge application* ジョブテンプレートを起動します。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Deploy edge application` <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックしてテンプレートを起動します。
* デフォルトの `Dublin region` を選択したままにし、`Next` ボタンをクリックします。
<a href="#Deploy app template region prompt">
  <img alt="アプリテンプレートリージョンプロンプトのデプロイ" src="../assets/img/deploy_app_template_prompt.png" />
</a>

<a href="#" class="lightbox" id="Deploy app template region prompt">
  <img alt="アプリテンプレートリージョンプロンプトのデプロイ" src="../assets/img/deploy_app_template_prompt.png" />
</a>

* 設定をプレビューし、`Launch` ボタンを押して自動化ジョブをトリガーします。

<a href="#Launch Deploy app template">
  <img alt="Deploy アプリテンプレートを起動する" src="../assets/img/deploy_app_template_launch.png" />
</a>

<a href="#" class="lightbox" id="Launch Deploy app template">
  <img alt="Deploy アプリテンプレートを起動する" src="../assets/img/deploy_app_template_launch.png" />
</a>

>ℹ️ `Deploy app テンプレート` は、情報収集、テンプレート作成、コンテナーイメージのプル、サービスの再起動など、複数のタスクを実行します。**Jobs** 内の **Views** セクションで実行されたすべてのタスクを確認します。

<a href="#View Deploy app template job execution">
  <img alt="アプリテンプレートのデプロイジョブの実行の表示" src="../assets/img/deploy_app_template_job.png" />
</a>

<a href="#" class="lightbox" id="View Deploy app template job execution">
  <img alt="アプリテンプレートのデプロイジョブの実行の表示" src="../assets/img/deploy_app_template_job.png" />
</a>


☑️ 最終タスク - Dublin HMI アプリケーションにログインする
===
* _Dublin app_ タブをクリックして、Ignition アプリケーションにログインします。
<a href="#Dublin App">
  <img alt="ダブリンアプリ" src="../assets/img/dublin-app.png" />
</a>

<a href="#" class="lightbox" id="Dublin App">
  <img alt="ダブリンアプリ" src="../assets/img/dublin-app.png" />
</a>

* 上記の管理者認証情報を使用してアプリケーションにログインします。

<a href="#Ignition Login">
  <img alt="Ignition ログイン" src="../assets/img/Ignition_login.png" />
</a>

<a href="#" class="lightbox" id="Ignition Login">
  <img alt="Ignition ログイン" src="../assets/img/Ignition_login.png" />
</a>

* アラートを破棄します。クイックスタートポップアップが表示された場合は、`No thanks` オプションを選択します。このラボでは産業用アプリケーションを設定しません。

<a href="#Ignition Quick Start">
  <img alt="Ignition クイックスタート" src="../assets/img/nothanks.png" />
</a>

<a href="#" class="lightbox" id="Ignition Quick Start">
  <img alt="Ignition クイックスタート" src="../assets/img/nothanks.png" />
</a>

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


