---
slug: playbook-files
id: ygraurb2blog
type: challenge
title: 'Playbook のさらなる拡張: ファイルのコピー'
teaser: '自動化を使用した他の内容の実行: ファイルの管理'
注記:
- type: text
  内容: ターゲットノードでの純粋な対話に加えて、
    制御インスタンスと管理対象ノードの間でデータをコピーする可能性もあります。コピー
    モジュールは、データの転送に使用できます。
タブ:
- title: エディター
  type: service
  hostname: control
  path: /editor/
  port: 443
- title: コントロール
  type: terminal
  hostname: control
難易度: 基本
時間制限: 1
---
👋 はじめに
===
#### 推定所要時間: *8 分*<p>
この課題では、`web.html` というラベルの付いた単純な Web ページを作成し、`curl` コマンドを使用してそのコンテンツを表示します。

☑️ タスク 1 - Files ディレクトリーの作成
===
* *editor* タブがデフォルトで開きます。

エディターで、ディレクトリー `ansible-files` の下にファイルディレクトリー `files` を作成します。これを行うには、右クリックして `New Folder` を選択します。


☑️ タスク 2 - web.html ファイルの作成
===

`files` ディレクトリー内で右クリックし、新しいファイルを選択して、次の内容の `web.html` というラベルの付いた HTML ファイルを作成します。

```
<body>
<h1>Apache is running fine, thanks to Ansible!</h1>
</body>
```

☑️ タスク 3 - apache.yml の更新
===

`apache.yml` ファイル内で `ansible.builtin.copy` モジュールを使用して、`web.html` ファイルを `node1` ホスト内の `/var/www/html/index.html` にコピーします。

>### **❗️注意❗️**
>タスクが前のタスクと同じようにインデントされていることを確認してください!


```
  - name: copy web.html
    ansible.builtin.copy:
      src: web.html
      dest: /var/www/html/index.html
```

ソースがディレクトリー `ファイル` について言及していないことに注意してください。`files` ディレクトリーは、管理しているホストに渡す ansible ファイルをデフォルトで保存する場所です。


☑️ タスク 4 - apache.yml Playbook の実行
===

*control* タブ内で、ディレクトリー `ansible-files` に変更し、Playbook を再度実行します。

```
cd ansible-files
```
```
ansible-navigator run apache.yml
```

☑️ タスク 5 - node1 の web.html の内容確認
===

Apache `node1` の `index.html` (デフォルトページ) にアクセスする `curl` コマンドは、次のように実行できます。

```
curl http://node1
```

```
<body>
    <h1>Apache is running fine, thanks to Ansible!</h1>
    </body>
```

✅ 次の課題
===
以下の `Check` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

🐛 問題が発生していますか ?
====

問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成](https://github.com/ansible/instruqt/issues/new?labels=writing-first-playbook&title=Issue+with+Writing+First+Playbook+slug+ID:+playbook-files&assignees=rlopez133)してください 。

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