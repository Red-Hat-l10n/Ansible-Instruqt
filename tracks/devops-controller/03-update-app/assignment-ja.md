---
slug: update-app
id: jixtci9el84k
type: challenge
title: Lets's Quiz! アプリケーションコードの更新
teaser: DevOps のワークフロー
  ビルドをトリガーするために、Let's Quiz! アプリケーションのホームページを更新します。
注記:
- type: text
  内容: |-
    # チャレンジの概要
    このチャレンジでは、ACME Corp の *Let's Quiz!* アプリケーションコードを更新し、
    変更を ACME Corp のソースコードリポジトリーにプッシュすることでパイプラインを開始します。

    ![env_tools](../assets/img/slides_3_update_app.png)

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
- title: Let's Quiz!
  type: service
  hostname: controller
  port: 8000
- title: VS Code
  type: service
  hostname: controller
  path: /editor/?folder=/home/rhel/acme_corp
  port: 443
- title: Jenkins
  type: service
  hostname: jenkins
  path: /job/ACMECorp/
  port: 8080
- title: Gitea
  type: service
  hostname: gitea
  path: /student/acme_corp
  port: 3000
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

ACME Corp は、_Let's Quiz!_ アプリケーションのホームページを更新する必要があります。このチャレンジでは、VS Code でアプリケーションを更新し、最初の _環境概要_ チャレンジで説明した Gitea webhook をトリガーします。

>### **❗️ 注記**
> このチャレンジのチェックは、Jenkins パイプラインの完了時間に変動が生じる可能性があるため、数秒長くかかる場合があります。

☑️ タスク 1 - 現在の Let's Quiz! アプリケーションのステータス
===

現在、*Let's Quiz!* アプリケーションは実稼働環境にはデプロイされていません。これについては、_Let's Quiz!_ タブの以下のメッセージで確認することができます。

* _Let’s Quiz!_ タブはデフォルトで開いているはずです。

<!-- ![App prerelease](../assets/img/app_page_prerelease.png) -->
<a href="#app_page_prerelease">
  <img alt="App prerelease"" src="../assets/img/app_page_prerelease.png" />
</a>

<a href="#" class="lightbox" id="app_page_prerelease">
  <img alt="App prerelease" src="../assets/img/app_page_prerelease.png" />
</a>

☑️ タスク 2 - ACME Corp ホームページの更新
===

ACME Corp のホームページを更新しましょう。

* ブラウザーウィンドウの上部にある _VS Code_ タブを開きます。
* VS Code Explorer ペインで、`app ⇒ lets_quiz ⇒ templates ⇒ quiz` に移動し、`home.html` をクリックします。

<!-- ![VSCode home.html](../assets/img/vscode_home_edit.png) -->
<a href="#vscode_home_edit">
  <img alt="VSCode home.html" src="../assets/img/vscode_home_edit.png" />
</a>

<a href="#" class="lightbox" id="vscode_home_edit">
  <img alt="VSCode home.html" src="../assets/img/vscode_home_edit.png" />
</a>

**`home.html` の `<!-- FIX ME -->` コメントの直下にある行を編集します。**

* 以下の行をコピーして貼り付け、`<!-- FIX ME -->` コメントのすぐ下にある既存の行を置き換えます。

```html
          <p class="display-4 d-none d-sm-block">The latest and greatest version of the app deployed successfully.</p>
```

新しい行は、以下のスクリーンショットのように表示されます。

<!-- ![home.html edited](../assets/img/vscode_home_edit_note.png) -->
<a href="#vscode_home_edit_note">
  <img alt="VSCode home.html" src="../assets/img/vscode_home_edit_note.png" />
</a>

<a href="#" class="lightbox" id="vscode_home_edit_note">
  <img alt="VSCode home.html" src="../assets/img/vscode_home_edit_note.png" />
</a>

>### **❗️ 注記**
> `home.html` の更新された行には、`<!-- FIX ME -->` コメントと同じインデントが必要です。異なる場合は、チャレンジチェックは失敗します。

* VS Code メニューバーの `File ⇒ Save` をクリックするか、関連するキーボードショートカットをクリックして、ファイルを保存します。


☑️ タスク 3 - コードをコミットしてプッシュし、パイプラインを開始する
===

**更新された `home.html` ファイルを _Gitea_ リポジトリーにコミットしてプッシュします。**

> ### **❗️ コードのコミットについてさらにガイダンスが必要ですか?**<p>
> 詳細な手順については、[Visual Studio Code Version Control ドキュメント](https://code.visualstudio.com/docs/editor/versioncontrol#_commit) を参照してください。

* 左側の VS Code Explorer ペインで、ナンバーバナーが付いた `Source Control` Git アイコンをクリックします。以下の画像では、ナンバーバナーは `1` になります。
* `home.html` ファイルの右側にある + 記号をクリックします。
* `Message` テキスト入力にコミットメッセージを入力します。たとえば、コミットメッセージは以下のようになります。

```
Updated home.html
```

* ☑️ をクリックして変更をコミットします。

<!-- ![VSCode commit](../assets/img/vscode_commit.png) -->
<a href="#vscode_commit">
  <img alt="VSCode" src="../assets/img/vscode_commit.png" />
</a>

<a href="#" class="lightbox" id="vscode_commit">
  <img alt="VSCode" src="../assets/img/vscode_commit.png" />
</a>

* 新しい `Sync Changes` ボタンが表示されます。これをクリックして、コードを ACME Corp リポジトリーにプッシュします。

<!-- ![VSCode commit](../assets/img/vscode_push.png) -->
<a href="#vscode_push">
  <img alt="VSCode" src="../assets/img/vscode_push.png" />
</a>

<a href="#" class="lightbox" id="vscode_push">
  <img alt="VSCode" src="../assets/img/vscode_push.png" />
</a>

>### **❗️ 注記**
> VS Code を使用してリポジトリーを同期する際にエラーが発生した場合は、以下の手順を試してください。
> * トップメニューにある `Terminal ==> New Terminal` をクリックして、*VS Code* で新しいターミナルを開きます。
> * 以下のコマンドをコピーしてターミナルに貼り付けます。
>
> ```bash
> git pull origin main --rebase
> ```
> * ファイルの競合があれば解決し、以下のコマンドを実行してリポジトリーを更新します。
>  ```bash
> git push origin main --force
> ```

☑️ タスク 4 - パイプラインステータスの確認
===

***Gitea* webhook がパイプラインを開始したかどうかを見てみましょう。**

* ブラウザーウィンドウの上部にある _Jenkins_ タブをクリックします。
* _Pipeline ACMECorp_ ウィンドウに、_Gitea_ webhook がパイプラインを開始したことが表示されます。
* *number* アイコンをクリックして、Jenkins ビルドを開きます。以下のスクリーンショットでは、ビルド番号は `1` です。

<!-- ![Jenkins running](../assets/img/jenkins_acme_job_running.png) -->
<a href="#jenkins_acme_job_running">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_job_running.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acme_job_running">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_job_running.png" />
</a>

* 次に、新しいウィンドウの左側のペインにある `Console Output` ボタンをクリックします。

<!-- ![Jenkins running](../assets/img/jenkins_acme_console_button.png) -->
<a href="#jenkins_acme_console_button">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_console_button.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acme_console_button">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_console_button.png" />
</a>

パイプラインは新しいパッケージバージョンを正常に作成し、自動コントローラー `DevOps Workflow` ジョブテンプレートを開始しました。

<!-- ![Jenkins running](../assets/img/jenkins_acme_console_bottom.png) -->
<a href="#jenkins_acme_console_bottom">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_console_bottom.png" />
</a>

<a href="#" class="lightbox" id="jenkins_acme_console_bottom">
  <img alt="Jenkins" src="../assets/img/jenkins_acme_console_bottom.png" />
</a>

`tag_name` 変数には、最新の _Let’s Quiz!_ アプリケーションバージョンが含まれています。上のイメージでは、`tag_name` 変数が `2.52.0` に設定されています。以下のチャレンジでは、コントローラーで `tag_name` 変数を使用します。

>**❗️ 注記**
>ラボのこの段階では、パイプラインは終了しません。次回のチャレンジでは、DevOps のワークフローを引き続きご紹介します。

☑️ タスク 5 - ACME Corp リポジトリーの確認
===

**_Gitea_ でホストされている ACME Corp リポジトリーを見てみましょう。**

* ブラウザーウィンドウの上部にある _Gitea_ タブをクリックします。
* ページの右上にある ↻ をクリックするか、ブラウザーを使用して Web ページを更新して、*Gitea* タブウィンドウを更新します。

<!-- ![Gitea updated](../assets/img/gitea_new_tag.png) -->
<a href="#gitea_new_tag">
  <img alt="Gitea" src="../assets/img/gitea_new_tag.png" />
</a>

<a href="#" class="lightbox" id="gitea_new_tag">
  <img alt="Gitea" src="../assets/img/gitea_new_tag.png" />
</a>

Jenkins コミットメッセージには、最新のバージョン番号が表示されます。以下のスクリーンショットでは、コミットメッセージは `Bump version from v2.51.0 to v2.52.0` となっています。

* 右隅の `Tags` ボタンをクリックします。

<!-- ![Gitea tag](../assets/img/gitea_tag_artifacts.png) -->
<a href="#gitea_tag_artifacts">
  <img alt="Gitea" src="../assets/img/gitea_tag_artifacts.png" />
</a>

<a href="#" class="lightbox" id="gitea_tag_artifacts">
  <img alt="Gitea" src="../assets/img/gitea_tag_artifacts.png" />
</a>

_Gitea_ は、新しいタグに関連付けられた `ZIP` および `TAR.GZ` ファイルを作成しました。上のスクリーンショットでは、タグ名は `v2.52.0` です。

このタグ番号とアーティファクトを次のチャレンジで使用します。

✅ 次のチャレンジ
===
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
