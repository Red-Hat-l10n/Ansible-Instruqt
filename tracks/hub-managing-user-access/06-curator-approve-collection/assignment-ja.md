---
slug: curator-approve-collection
id: flbyvg1ed1zo
type: challenge
title: コレクションをキュレーターとして承認
teaser: このチャレンジでは、キュレーターによるインポートログの確認方法と、Private Automation Hub でのコレクションの承認/拒否方法を説明します
  
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

このチャレンジでは、**curator** ユーザーとしてログインし、前のチャレンジでプッシュされたコレクションを承認および公開します。

☑️ タスク 1 - キュレーターユーザーとしてコレクションを承認する
===

* `automationhub-web` タブに **curator** ユーザーとしてログインします。
* 以下のスクリーンショットで、キュレーターがインポートログを確認し、コレクションを承認または拒否する方法を確認します。

<!-- ![View Import Logs](../assets/view_import_logs.png
) -->
<a href="#view_import_logs">
  <img alt="インポートログの表示" src="../assets/view_import_logs.png" />
</a>
<a href="#" class="lightbox" id="view_import_logs">
  <img alt="インポートログの表示" src="../assets/view_import_logs.png" />
</a>

<!-- ![Approve Collection](../assets/approve_collections.png
) -->
<a href="#approve_collection">
  <img alt="コレクションの承認" src="../assets/approve_collections.png" />
</a>
<a href="#" class="lightbox" id="approve_collection">
  <img alt="コレクションの承認" src="../assets/approve_collections.png" />
</a>

* コレクションが承認されたら、**curator** としてログアウトします。

<!-- ![Curator Logout](../assets/curator_logout.png
) -->
<a href="#curator_logout">
  <img alt="Curator のログアウト" src="../assets/curator_logout.png" />
</a>
<a href="#" class="lightbox" id="curator_logout">
  <img alt="Curator のログアウト" src="../assets/curator_logout.png" />
</a>


☑️ タスク 2 - marie/bob ユーザーとしてログインしてコレクションが公開されているか確認する
===

* curator ユーザーとしてログアウトします。
* **marie** としてログインし、コレクションが公開されているか確認します (以下のスクリーンショット参照)。

<!-- ![Check Collections](../assets/marie_user_show_collections.png
) -->
<a href="#check_collections">
  <img alt="コレクションの確認" src="../assets/marie_user_show_collections.png" />
</a>
<a href="#" class="lightbox" id="check_collections">
  <img alt="コレクションの確認" src="../assets/marie_user_show_collections.png" />
</a>

☑️ まとめ
===
* キュレーターは、インポートログに基づきコレクションを承認または拒否できます。
* コレクションが公開されると、すべてのユーザーは Private Automation Hub からコレクションを表示およびダウンロードできます。

✅ 終了
===
これは、このラボの終わりを示します。これで Private Automation Hub についての学習が完了しました。

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