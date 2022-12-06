---
slug: playbook-variables
id: ud5t6go9cbs0
type: challenge
title: ミックスへの変数追加
teaser: Ansible は、Playbook で使用できる値を格納するための変数をサポートしています。 では
  やってみましょう。
注記:
- type: text
  内容: Ansible は、Playbook で使用できる値を格納するための変数をサポートしています。
    変数はさまざまな場所で定義でき、明確な優先順位があります。Ansible
    は、タスクの実行時に変数をその値に置き換えます。
- type: text
  内容: |-
    変数は、変数名を二重中括弧で囲むことにより、AnsiblePlaybooks で参照されます。

    ```
    Here comes a variable {{ variable1 }}
    ```
- type: text
  内容: 変数とその値は、インベントリー、
    追加のファイル、コマンドラインなどのさまざまな場所で定義できます。
- type: text
  内容: |-
    インベントリーに対して変数を指定する推奨の方法として、`host_vars` および `group_vars` という名前の 2 つのディレクトリーにあるファイルで変数を定義します。

    * グループ servers の変数を定義するために、変数定義を含む `group_vars/servers.yml` という名前の YAML ファイルが作成されます。
    * ホスト host node1 専用の変数を定義するために、変数定義のある `host_vars/node1.yml` ファイルが作成されます。
- type: text
  内容: ホスト変数はグループ変数よりも優先されます (優先順位
    の詳細は [docs](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable) を参照してください)。
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
#### 推定所要時間: *10 分*<p>
この課題では、異なる場所 `group_vars` および `host_vars` で指定された変数の使用に慣れます。場所ごとに異なる動作が提供されます。

☑️ タスク 1 - 変数ディレクトリーの作成
===

このタスクでは、`ansible-files` 内に `group_vars` と `host_vars` の 2 つのディレクトリーを作成します。右クリックして新しいフォルダーを選択し、それぞれを作成します。

目的は、指定されたホストとグループ全体のさまざまな変数を保存することです。

☑️ タスク 2: group_vars/web.yml ファイルの作成
===

以下の内容で `~/ansible-files/group_vars/web.yml` ファイルを作成します。

```
---
stage: dev
```

`group_vars/web.yml` ファイルは、値 `dev` を `stage` というラベルの付いた変数に渡します。

☑️ タスク 3 - host_vars/node1.yml ファイルの作成
===

次の内容で `~/ansible-files/host_vars/node1.yml` ファイルを作成します。

```
---
stage: prod
```

`host_vars/node1.yml` ファイルは、値 `prod` を `stage` というラベルの付いた変数に渡します。

☑️ タスク 4 - web.html ステージファイルの作成
===

選択されたステージ変数に応じて、Ansible Playbook は異なる web.html ファイルをコピーします。

2 つのステージファイルを作成しましょう。最初に以下の内容を含む `~/ansible-files/files/prod_web.html` ファイル を作成します。

```
<body>
<h1>This is a production webserver, take care!</h1>
</body>
```

次に、以下の内容を含む `~/ansible-files/files/dev_web.html` ファイルを作成します。

```
<body>
<h1>This is a development webserver, have fun!</h1>
</body>
```

☑️ タスク 5 - ステージ変数を使用した apache.yml Playbook の変更
===

既存の `apache.yml Playbook` のコピータスクを次のように変更します。

```
  - name: copy web.html
    ansible.builtin.copy:
      src: "{{ stage }}_web.html"
      dest: /var/www/html/index.html
```

☑️ タスク 6 - apache.yml Playbook の実行
===

*control* タブ内で、Playbook を実行します。

```
cd ansible-files
```

```
ansible-navigator run apache.yml
```

☑️ タスク 7 - 結果の確認
===

`node1` サーバーは、実動 Web ページを指している必要があります。`node2` サーバーは、開発 Web ページを指している必要があります。

```
curl http://node1
```
```
<body>
    <h1>This is a production webserver, take care!</h1>
    </body>
```

```
curl http://node2
```

```
<body>
    <h1>This is a development webserver, have fun!</h1>
    </body>
```

✅ 次の課題
===
以下の `Check` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

🐛 問題が発生していますか ?
====

問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] してください (https://github.com/ansible/instruqt/issues/new?labels=writing-first-playbook&title=Issue+with+Writing+First+Playbook+slug+ID:+playbook-variables&assignees=rlopez133)。

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