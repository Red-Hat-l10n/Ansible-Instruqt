---
slug: create-cloud-namespace-group
id: uvnqtjerjz7s
type: challenge
title: Private Automation Hub のクラウド名前空間とグループの作成
teaser: Private Automation Hub のクラウド名前空間に Ansible コンテンツコレクションをアップロードするためのアクセス権を持つクラウドユーザーグループとユーザー marie を作成します。
  
  
tabs:
- title: automationhub-web
  type: service
  hostname: privatehub-01
  path: /
  port: 443
難易度: 基本
制限時間: 400
---

🔐 ログイン認証情報

>ユーザー: curator<p>
>パスワード: learn_ansible

☑️ タスク 1 - Cloud Automation ユーザーグループを作成する
===

Curator は、クラウド自動化チーム向けに **Cloud Automation** というユーザーグループを作成したいと考えています。Curator は、**Cloud Automation** ユーザーグループが、コレクションをクラウド名前空間のみにアップロードするパーミッションを持っていることを確認する必要があります。

以下の手順に従って、クラウドユーザーグループを作成してください。

1. automationhub-web タブで、*curator* ユーザーとしてログインしていることを確認します。
2. 左側のペインで User Access > Groups をクリックします。
3. Create ボタンをクリックします。
<!-- ![Group Create Cloud Button](../assets/create_button_group_cloud.png) -->
<a href="#group_create_cloud_button">
  <img alt="Group Create Cloud ボタン" src="../assets/create_button_group_cloud.png" />
</a>
<a href="#" class="lightbox" id="group_create_cloud_button">
  <img alt="Group Create Cloud ボタン" src="../assets/create_button_group_cloud.png" />
</a>
4.グループ名に Cloud Automation と入力し、Create ボタンをクリックします。
<!-- ![Group Create Cloud](../assets/create_dialog_group_cloud.png) -->
<a href="#group_create_cloud">
  <img alt="Group Create Cloud" src="../assets/create_dialog_group_cloud.png" />
</a>
<a href="#" class="lightbox" id="group_create_cloud">
  <img alt="Group Create Cloud" src="../assets/create_dialog_group_cloud.png" />
</a>
5.グループを作成するとパーミッションページが表示され、ここでパーミッションを割り当てることができます。Edit をクリックします。パーミッションを編集して、グループに Upload to namespace パーミッションを追加します。Save をクリックします。
<!-- ![Group Create Cloud](../assets/cloud_group_permissions.png) -->
<a href="#cloud_group_permissions">
  <img alt="Cloud グループのパーミッション" src="../assets/cloud_group_permissions.png" />
</a>
<a href="#" class="lightbox" id="cloud_group_permissions">
  <img alt="Cloud グループのパーミッション" src="../assets/cloud_group_permissions.png" />
</a>


☑️ タスク 2 - Cloud Automation グループでユーザー marie を作成する
===
1. 左側のペインで User Access > Users をクリックします。
<!-- ![Create User Marie](../assets/create_user_marie.png) -->
<a href="#create_user_marie_button">
  <img alt="Create User Marie ボタン" src="../assets/create_user_marie.png" />
</a>
<a href="#" class="lightbox" id="create_user_marie_button">
  <img alt="Create User Marie ボタン" src="../assets/create_user_marie.png" />
</a>
2.username フィールドを marie に、password フィールドを learn_ansible に設定し、ユーザー marie に Cloud Automation グループを割り当てます。
<!-- ![Create User Marie Dialog](../assets/create_user_marie_dialog.png) -->
<a href="#create_user_marie_dialog">
  <img alt="Create User Marie ダイアログ" src="../assets/create_user_marie_dialog.png" />
</a>
<a href="#" class="lightbox" id="create_user_marie_dialog">
  <img alt="Create User Marie ダイアログ" src="../assets/create_user_marie_dialog.png" />
</a>

☑️ タスク 3 - クラウド名前空間の作成
===
1. 左側のペインで Collections > Namespaces をクリックし、Namespace メニューに移動します。
<!-- ![Namespace Menu](../assets/namespace_menu.png) -->
<a href="#namespace_menu">
  <img alt="Namespace メニュー" src="../assets/namespace_menu.png" />
</a>
<a href="#" class="lightbox" id="namespace_menu">
  <img alt="Namespace メニュー" src="../assets/namespace_menu.png" />
</a>
2.Create ボタンをクリックし、新規名前空間を作成します。
<!-- ![Namespace Create Button](../assets/namespace_create_button.png) -->
<a href="#namespace_create_button">
  <img alt="Namespace Create ボタン" src="../assets/namespace_create_button.png" />
</a>
<a href="#" class="lightbox" id="namespace_create_button">
  <img alt="Namespace Create ボタン" src="../assets/namespace_create_button.png" />
</a>
3.ダイアログで、名前空間名を cloud に設定し、その名前空間の所有者を Cloud Automation グループに設定します。
<!-- ![Namespace Create Dialog 1](../assets/namespace_create_cloud_dialog1.png) -->
<a href="#namespace_create_dialog1">
  <img alt="Namespace Create ダイアログ 1" src="../assets/namespace_create_cloud_dialog1.png" />
</a>
<a href="#" class="lightbox" id="namespace_create_dialog1">
  <img alt="Namespace Create ダイアログ 1" src="../assets/namespace_create_cloud_dialog1.png" />
</a>
4.Change Namespace パーミッションを削除して Cloud グループの Upload to Namespace パーミッションのみ残し、Create ボタンをクリックしてデフォルトのパーミッションを変更します。
<!-- ![Namespace Create Dialog 2](../assets/namespace_create_cloud_dialog2.png) -->
<a href="#namespace_create_dialog2">
  <img alt="Namespace Create ダイアログ 2" src="../assets/namespace_create_cloud_dialog2.png" />
</a>
<a href="#" class="lightbox" id="namespace_create_dialog2">
  <img alt="Namespace Create ダイアログ 2" src="../assets/namespace_create_cloud_dialog2.png" />
</a>
5.Curator ユーザーからログアウトします。
<!-- ![Curator Logout](../assets/curator_logout.png) -->
<a href="#curator_logout">
  <img alt="Curator のログアウト" src="../assets/curator_logout.png" />
</a>
<a href="#" class="lightbox" id="curator_logout">
  <img alt="Curator のログアウト" src="../assets/curator_logout.png" />
</a>

☑️ タスク 4 - クラウドグループのユーザー marie としてログインする
===
Private Automation Hub インスタンスの Cloud グループからユーザー marie としてログインします。
<br>
🔐 ログイン認証情報

>ユーザー: marie<p>
>パスワード: learn_ansible
<!-- ![Marie Login](../assets/marie_login.png
) -->
<a href="#marie_login">
  <img alt="Marie のログイン" src="../assets/marie_login.png" />
</a>
<a href="#" class="lightbox" id="marie_login">
  <img alt="Marie のログイン" src="../assets/marie_login.png" />
</a>

* ユーザー marie は、左ペインの User Access オプションにアクセスできないため、ユーザーまたはグループを編集できないことに注意してください。

☑️ タスク 5 - marie ユーザーからログアウトする
===
* 次のチャレンジで network グループに新しいユーザー Bob を作成するため、ユーザー marie からログアウトします。


☑️ まとめ
===
* Cloud Automation グループと、そのグループのユーザー marie を作成しました。
* このグループには、名前空間を変更して名前空間にアップロードできるパーミッションがあります。
* このグループは、Private Automation Hub の cloud 名前空間の所有者です。

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