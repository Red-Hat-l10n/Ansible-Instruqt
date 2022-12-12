---
slug: playbook-templates
id: jr7lijnkrpdy
type: challenge
title: テンプレート
teaser:テンプレートを使用すると、同じファイルから複数のホスト固有の設定を作成できます
  。
注記:
- type: text
  コンテンツ: Ansible は、ファイルが管理対象ホストに配布される前に、[inja2](http://jinja.pocoo.org/) 
    テンプレートを使用してファイルを変更します。Jinja2 は、Python 
    で最も使用されているテンプレートエンジンの 1 つです。
- type: text
  コンテンツ: ファイルのテンプレートが作成されると、コントロールノードから
    管理対象ホストへのローカルファイルの転送をサポートするテンプレートモジュールを使用して、
    管理対象ホストにデプロイできます。
- type: text
  内容: ファイルがテンプレートファイルであることを示すファイルの末尾は 
    `.j2` です。これは厳密に言えば必要ではありませんが、このプラクティスは確立されています。
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
#### 推定所要時間: *7 分*<p>
この課題では、Jinja2 テンプレートを作成します。Ansible は、ファイルが管理対象ホストに配布される前に、Jinja2 テンプレートを使用してファイルを変更します。Jinja2 は、Python で最も使用されているテンプレートエンジンの 1 つです (http://jinja.pocoo.org/)。


☑️ タスク 1 - テンプレートディレクトリーの作成
===
* *editor* タブがデフォルトで開きます。

*editor* タブで、ディレクトリー `templates` を作成し (右クリックして新しいフォルダーを選択)、`~/ansible-files/` の下にテンプレートリソースを保持します。

☑️ タスク 2 - motd-facts.j2 jinja ファイルの作成
===

`ansible-files/templates` ディレクトリー内で、ファイル `motd-facts.j2` を作成します。

```
Welcome to {{ ansible_hostname }}.
{{ ansible_distribution }} {{ ansible_distribution_version}}
deployed on {{ ansible_architecture }} architecture.
```

テンプレートファイルには、後でホストにコピーされる基本的なテキストが含まれています。これには、ターゲットマシンで個別に置き換えられる変数が含まれています。

☑️ タスク 2 - motd-facts.yml Playbook の作成
===

新しく作成したテンプレートファイルを使用する Ansible Playbook を作成します。`ansible-files` フォルダーの *editor* タブ内で、右クリックして 新しいファイルを選択し、`motd-facts.yml` を作成します。

```
---
- name: Fill motd file with host data
  hosts: node1
  become: true
  tasks:
    - ansible.builtin.template:
        src: motd-facts.j2
        dest: /etc/motd
        owner: root
        group: root
        mode: 0644
```

☑️ タスク 3 - motd-facts.yml Playbook の実行
===

*control* タブで、`motd-facts.yml Playbook` を実行します。

```
cd ansible-files
```
```
ansible-navigator run motd-facts.yml
```

☑️ タスク 4 - 今日のメッセージの確認
===

SSH 経由で `node1` にログインし、その日の内容のメッセージを確認します。

```
ssh node1
```
```
Welcome to node1.
RedHat 8.5
deployed on x86_64 architecture.
```

✅ 次の課題
===
以下の `Check` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

🐛 問題が発生していますか ?
====

問題が発生した場合や、正しくない点に気付いた場合は、[open an issue](https://github.com/ansible/instruqt/issues/new?labels=writing-first-playbook&title=Issue+with+Writing+First+Playbook+slug+ID:+playbook-templates&assignees=rlopez133)をクリックしてください。

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