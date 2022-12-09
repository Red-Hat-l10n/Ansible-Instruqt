---
slug: create-network-namespace-group
id: rk3hstxlzehy
type: challenge
title: Private Automation Hub のネットワーク名前空間とグループの作成
teaser: Private Automation Hub のネットワーク名前空間に Ansible コンテンツコレクションをアップロードするためのアクセス権を持つネットワークユーザーグループとユーザー Bob を作成します。
  
  
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
制限時間: 400
---

🔐 ログイン認証情報

>ユーザー: curator<p>
>パスワード: learn_ansible

前のチャレンジとよく似ていますが、ここでは別のグループ、ユーザー、名前空間を作成します。詳細は以下を参照してください。
1. グループ名 - **Network Automation**
2. ユーザー名 - **bob**
3. 名前空間 - **network**

☑️ タスク 1 - ネットワークユーザーグループを作成する
===

Curator は、ネットワーク自動化チーム向けに *Network Automation* というユーザーグループを作成したいと考えています。Curator は、このクラウドユーザーグループが、コレクションを **network** 名前空間のみにアップロードするパーミッションを持っていることを確認する必要があります。

以下の手順に従って、**Network Automation** を作成してください。

1. automationhub-web タブで、*curator* ユーザーとしてログインしていることを確認します。
2. ログイン後、左側のペインで User Access > Groups をクリックします。
3. Create ボタンをクリックします。
<!-- ![Group Create Network Button](../assets/create_button_group_network.png) -->
<a href="#group_create_network_button">
  <img alt="Group Create Network ボタン" src="../assets/create_button_group_network.png" />
</a>
<a href="#" class="lightbox" id="group_create_network_button">
  <img alt="Group Create Network ボタン" src="../assets/create_button_group_network.png" />
</a>
4.グループ名に Network Automation と入力し、Create ボタンをクリックします。
<!-- ![Group Create Network](../assets/create_dialog_group_network.png) -->
<a href="#group_create_network">
  <img alt="Group Create Network" src="../assets/create_dialog_group_network.png" />
</a>
<a href="#" class="lightbox" id="group_create_network">
  <img alt="Group Create Network" src="../assets/create_dialog_group_network.png" />
</a>
5.グループを作成するとパーミッションページが表示され、ここでパーミッションを割り当てることができます。Edit をクリックします。パーミッションを編集して、グループに Upload to namespace パーミッションを追加します。Save をクリックします。
<!-- ![Group Create Network](../assets/network_group_permissions.png) -->
<a href="#network_group_permissions">
  <img alt="Network グループのパーミッション" src="../assets/network_group_permissions.png" />
</a>
<a href="#" class="lightbox" id="network_group_permissions">
  <img alt="Network グループのパーミッション" src="../assets/network_group_permissions.png" />
</a>


☑️ タスク 2 - ネットワークグループにユーザー bob を作成する
===
1. 左側のペインで User Access > Users をクリックします。
<!-- ![Create User Bob](../assets/create_user_bob_button.png) -->
<a href="#create_user_bob_button">
  <img alt="Create User Bob ボタン" src="../assets/create_user_bob_button.png" />
</a>
<a href="#" class="lightbox" id="create_user_bob_button">
  <img alt="Create User Bob ボタン" src="../assets/create_user_bob_button.png" />
</a>
2.username フィールドを bob に、password フィールドを learn_ansible に設定し、ユーザー bob にそのグループを Network Automation グループとして割り当てます。
<!-- ![Create User Bob Dialog](../assets/create_user_bob_dialog.png) -->
<a href="#create_user_bob_dialog">
  <img alt="Create User Bob ダイアログ" src="../assets/create_user_bob_dialog.png" />
</a>
<a href="#" class="lightbox" id="create_user_bob_dialog">
  <img alt="Create User Bob ダイアログ" src="../assets/create_user_bob_dialog.png" />
</a>

☑️ タスク 3 - ネットワーク名前空間を作成する
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
<!-- ![Namespace Create Button2](../assets/namespace_create_button2.png) -->
<a href="#namespace_create_button2">
  <img alt="Namespace Create Button2" src="../assets/namespace_create_button2.png" />
</a>
<a href="#" class="lightbox" id="namespace_create_button2">
  <img alt="Namespace Create Button2" src="../assets/namespace_create_button2.png" />
</a>
3.ダイアログで、名前空間名を network に設定し、その名前空間の所有者を Network Automation グループに設定します。
<!-- ![Namespace Create Network Dialog 1](../assets/namespace_create_network_dialog1.png) -->
<a href="#namespace_create_network_dialog1">
  <img alt="Namespace Create Network ダイアログ 1" src="../assets/namespace_create_network_dialog1.png" />
</a>
<a href="#" class="lightbox" id="namespace_create_network_dialog1">
  <img alt="Namespace Create Network ダイアログ 1" src="../assets/namespace_create_network_dialog1.png" />
</a>
4.Change Namespace パーミッションを削除して Network Automation グループの Upload to Namespace パーミッションのみ残し、Create ボタンをクリックしてデフォルトのパーミッションを変更します。
<!-- ![Namespace Create Network Dialog 2](../assets/namespace_create_network_dialog2.png) -->
<a href="#namespace_create_network_dialog2">
  <img alt="Namespace Create Network ダイアログ 2" src="../assets/namespace_create_network_dialog2.png" />
</a>
<a href="#" class="lightbox" id="namespace_create_network_dialog2">
  <img alt="Namespace Create Network ダイアログ 2" src="../assets/namespace_create_network_dialog2.png" />
</a>
5.curator ユーザーからログアウトします。
<!-- ![Curator Logout](../assets/curator_logout.png) -->
<a href="#curator_logout">
  <img alt="Curator のログアウト" src="../assets/curator_logout.png" />
</a>
<a href="#" class="lightbox" id="curator_logout">
  <img alt="Curator のログアウト" src="../assets/curator_logout.png" />
</a>

☑️ タスク 4 - ネットワークグループのユーザー bob としてログインする
===
Private Automation Hub インスタンスの Network Automation グループからユーザー bob としてログインします。
🔐 ログイン認証情報

>ユーザー: bob<p>
>パスワード: learn_ansible
<!-- ![Bob Login](../assets/bob_login.png
) -->
<a href="#bob_login">
  <img alt="Bob のログイン" src="../assets/bob_login.png" />
</a>
<a href="#" class="lightbox" id="bob_login">
  <img alt="Bob のログイン" src="../assets/bob_login.png" />
</a>

* ユーザー bob は、左ペインの User Access オプションにアクセスできないため、ユーザーまたはグループを編集できないことに注意してください。

☑️ タスク 5 - ユーザー bob としてログアウトする
===
* 次のチャレンジに進む前に、必ずユーザー bob からログアウトしてください。


☑️ まとめ
===
* Network Automation グループと、そのグループのユーザー bob を作成しました。
* このグループには、名前空間を変更して名前空間にアップロードできるパーミッションがあります。
* このグループは、Private Automation Hub の cloud 名前空間の所有者です。

✅ 次の課題
===
タスクを完了したら、下の `Next` ボタンを押して次のチャレンジに進みます。

NORMAL で問題が発生していますか ?
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