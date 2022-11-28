---
slug: ansible-navigator-intro
id: rhdswz55nmob
type: challenge
title: 環境について
teaser: この課題では、ナビゲーターとコードエディターの環境の詳細を確認します。
注記:
- type: text
  コンテンツ: |-
    [`ansible-navigator`](https://github.com/ansible/ansible-navigator) は、Ansible Automation Platform サブスクライバーが利用できるテキストユーザーインターフェイス (TUI) であり、Ansible Automation Platform 2 で ansible Automation を作成およびテストするための主要なインターフェイスとして導入されました。
    <br><br><br>
    `ansible-navigator` は、他の `ansible-*` ユーティリティーの中でも、`ansible-playbook` のドロップイン代替としても機能し、Ansible Automation Platform 2 に移行する自動化を実行する標準的な方法です。
タブ:
- title: code-server
  type: service
  hostname: code-server
  path: /editor/?folder=vscode-remote%3A%2F%2F%2fhome%2Frhel
  port: 80
難易度: 基本
制限時間: 450
---
`ansible-navigator` は、一般的な開発者ワークフローに適合するように構築されており、[`code-server`](https://github.com/cdr/code-server) 統合ターミナル内から使用されます。***`code-server` は Ansible Automation Platform にパッケージ化されておらず、Red Hat とはまったく提携していないことに注意してください***

統合ターミナルを開きます `Terminal > New Terminal`


**1\.**ナビゲーターがインストールされていることをすばやくテストするには、次を実行します。
```
ansible-navigator --help
```

***

**2\.**`ansible-navigator` が正常にインストールされたことがわかったので、localhost に ping するための `test.yml` という名前の簡単な Playbook を作成してみてください。次のようになります。
```
---
- name: this is just a test
  hosts: localhost
  gather_facts: true
  tasks:

  - name: ping test
    ping:
```

**3\.**次に、`ansible-navigator` で実行します:
```
ansible-navigator run ./test.yml -m stdout
```
<br>
このようなものが表示されます (`ansible-playbook`出力のようなもの):

```
[rhel@code-server ~]$ ansible-navigator run ./test.yml -m stdout
[WARNING]: provided hosts list is empty, only localhost is available. Note that
the implicit localhost does not match 'all'

PLAY [this is just a test] *****************************************************

TASK [Gathering Facts] *********************************************************
ok: [localhost]

TASK [ping test] ***************************************************************
ok: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
<br>

***
**注:** `-m stdout` は標準出力モードで実行され、`ansible-playbook と` 同じように実行結果が表示されます
