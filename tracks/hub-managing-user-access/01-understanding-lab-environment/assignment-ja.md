---
slug: understanding-lab-environment
id: rxgbztqmrmnl
type: challenge
title: ラボ環境について
teaser: このチャレンジでは、コレクションの署名と検証のための
  ラボ環境設定を理解します。
注記:
- type: text
  コンテンツ: |2-

    # Private Automation Hub を使用したユーザーアクセスおよびコンテンツアップロードポリシーの管理
    ***

    このラボでは、主に 2 つのペルソナに焦点を当てて説明します。
    - Automation Curator - 組織の Private Automation Hub のコンテンツを管理します。キュレーターは、すべての自動化コンテンツのマネージャー/監督者です。
    - Automation Developer - 組織内の特定のグループ (ネットワーク、クラウド、またはストレージの自動化開発者など) に関連付けられている自動化開発者。グループの Ansible Automation を書き込みます。

    このラボで、キュレーターはクラウドおよびネットワーク自動化開発者に、コンテンツコレクションと自動化実行環境を Private Automation Hub インスタンスにプッシュするためのパーミッションを付与したいと考えています。

    これは実際のシナリオから着想を得ており、このラボのキュレーターを、テスト後に特定のグループからのコンテンツのみ公開する必要がある組織の自動化管理者とみなしています。

    このラボでは、次の内容について説明します。

    * Curator は、受信したコンテンツコレクションのポリシーを設定し、承認のためにコンテンツコレクションをテストおよび検証できるようにします。
    * コレクションをクラウドの名前空間に公開するためのアクセス権を持つ "Cloud Automation" グループを作成します。
    * コレクションをネットワークの名前空間に公開するためのアクセス権を持つ "Network Automation" グループを作成します。
    * クラウド自動化開発者は、コレクションをクラウドの名前空間に公開します。
    * ネットワーク自動化開発者は、コレクションをネットワークの名前空間に公開します。
    * Curator は、インポートログに基づき、クラウドおよびネットワークグループからのコレクションを承認します。
タブ:
- title: automationhub-web
  type: service
  hostname: privatehub-01
  path: /
  port: 443
- title: automationhub-terminal
  type: terminal
  hostname: privatehub-01
難易度: 基本
制限時間: 600
---

👋 はじめに
===
#### 推定所要時間: *5 分*<p>
ACME Corp は、組織全体でワークフローを自動化するために Ansible に大きく依存しています。Ansible コンテンツコレクションと自動化実行環境のライブラリーとして使用する Private Automation Hub インスタンスがあります。組織のグループは、この Private Automation Hub インスタンスのコレクションおよび実行環境を使用して自動化をテストします。

Private Automation Hub インスタンスは組織全体で自動化コンテンツライブラリーとして機能するため、ACME Corp は必ずテストと承認を経てコンテンツコレクションを Private Automation Hub インスタンスに公開します。承認されると、組織内の特定グループにのみコンテンツコレクションを Private Automation Hub にプッシュするためのアクセス権を付与します。

☑️ タスク 1 - ラボの前提を理解する
===

ACME Corp には、主に 3 つのユーザーグループがあります。
1. Automation Curators - アップロードテストを設定し、Private Automation Hub へのアクセスを管理します。
2. Cloud Automation - 組織のクラウドワークフローを自動化する Ansible コンテンツコレクションを作成します。自動化の例には、Amazon Web Services (AWS)、Microsoft Azure、Google Cloud Platform (GCP) からのクラウドインスタンスの管理や作成があります。
3. Network Automation - 組織のネットワークワークフローを自動化できるコンテンツコレクションを作成します。たとえば、複数のベンダー (Cisco、Juniper など) のスイッチとルーターを自動化および管理します。

* キュレーターは Automation Curators グループに属しており、Ansible コンテンツコレクションのアップロードポリシーを設定し、ユーザーである Bob (ネットワークグループ所属) および Marie (クラウドグループ所属) にアクセス権を設定します。

* Marie は ACME Corp のクラウド自動化エキスパートで、クラウド自動化コレクションを Private Automation Hub にプッシュしたいと考えています。

* Bob は ACME Corp の優れたネットワーク自動化エキスパートで、ACME Corp で使用されているさまざまなネットワークデバイスを自動化する Ansible コンテンツコレクションの構築方法を知っています。Bob は、ネットワークコレクションを Private Automation Hub にプッシュしたいと考えています。


☑️ タスク 2 - キュレーターユーザーとして Private Automation Hub にログインし、パーミッションを確認する
===

* *automationhub-web* タブが開き、デフォルトでログイン画面が表示されます。以下の認証情報を使用し、キュレーターユーザーとして Private Automation Hub にログインします。

🔐 ログイン認証情報

>ユーザー: curator<p>
>パスワード: learn_ansible

* ログインしたら、User Access をクリックし、Groups オプションを選択します。Automation Curators のラベルが付いた 1 つのグループのみ存在することを確認してください。このグループをクリックし、割り当てられたパーミッションを表示します。
<!-- ![User Access Tab](../assets/user_access_tab.png) -->
<a href="#user_access_tab">
  <img alt="User Access タブ" src="../assets/user_access_tab.png" />
</a>
<a href="#" class="lightbox" id="user_access_tab">
  <img alt="User Access タブ" src="../assets/user_access_tab.png" />
</a>

* User Access で Groups オプションをクリックし、存在するグループを確認します。Automation Curators という 1 つのグループのみが存在していることを確認し、それをクリックして割り当てられているパーミッションを表示します。
<!-- ![User Access groups](../assets/user_access_groups.png) -->
<a href="#user_access_groups">
  <img alt="User Access のグループ" src="../assets/user_access_groups.png" />
</a>
<a href="#" class="lightbox" id="user_access_groups">
  <img alt="User Access のグループ" src="../assets/user_access_groups.png" />
</a>

* Automation Curators グループに割り当てられたパーミッションを確認できます。Curator はこのグループに属し、Private Automation Hub にグループおよびユーザーを追加するパーミッションを持ちます。
<!-- ![Curator group permissions](../assets/curator_group_permissions.png) -->
<a href="#curator_group_permissions">
  <img alt="Curator グループのパーミッション" src="../assets/curator_group_permissions.png" />
</a>
<a href="#" class="lightbox" id="curator_group_permissions">
  <img alt="Curator グループのパーミッション" src="../assets/curator_group_permissions.png" />
</a>

* ここで User Access の下の左ペインで Users オプションをクリックすると、2 人のユーザーが表示されます。
  * **admin** \- デフォルトで作成されるスーパーユーザーで、すべてのパーミッションを持ち、Private Automation Hub に関連するすべてのオブジェクトの所有者です。*admin* ユーザーは、ラボの事前設定としてこのキュレーターを作成するために使用されます。
  * **curator**: Automation Curators グループに属し、この Private Automation Hub インスタンスを管理します。
  <!-- ![Curator User](../assets/curator_user.png) -->
<a href="#curator_user">
  <img alt="Curator ユーザー" src="../assets/curator_user.png" />
<a href="#" class="lightbox" id="curator_user">
  <img alt="Curator ユーザー" src="../assets/curator_user.png" />
</a>

☑️ タスク 3 - Private Automation Hub バックエンドにコンテンツアップロードポリシーを設定する
===
* 開いている *automationhub-terminal* タブをクリックし、次の手順に従いアップロードポリシーの設定方法を確認します。
* ターミナルで以下のコマンドを実行します。
  <br>
  ```
  cat /etc/galaxy-importer/galaxy-importer.cfg
  ```
  <br>
  2 つのオプションが設定されています。
  * RUN_ANSIBLE_TEST - このラボでは `ansible-test` の実行が対象外であるため False に設定されていますが、各コレクションアップロードで ansible-test を実行する場合はこれを True に設定します。
  * CHECK_REQUIRED_TAGS - このオプションは、アップロードされるコレクションに、Ansible コンテンツコレクションのタイプを指定する 1 つ以上のタグが必要であることを示します。

キュレーターは、`galaxy-importer.cfg` の編集後にコンテンツアップロードポリシーを決定できます。他のオプションについては、[Galaxy Importer Repository](https://github.com/ansible/galaxy-importer#configuration) を参照してください。

**注**: この Private Automation Hub インスタンスは、何かを公開する前に必ず承認を要求するように設定されており、キュレーターユーザーはコンテンツを承認できるパーミッションを持っています。

☑️ まとめ
===
* Curator は Automation Curator グループに属し、Private Automation Hub に公開するコンテンツを承認するパーミッションを持っています。
* アップロードされる Ansible コンテンツコレクションには、`galaxy-importer.cfg` ファイルに設定されているポリシーが適用されます。

✅ 次の課題
===
タスクを完了したら、下の `Next` ボタンを押して次のチャレンジに進みます。

🐛 問題が発生しましたか?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] (https://github.com/ansible/instruqt/issues/new) してください。

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
