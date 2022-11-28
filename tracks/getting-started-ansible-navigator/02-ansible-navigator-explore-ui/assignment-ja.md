---
slug: ansible-navigator-explore-ui
id: cjpyrstazxxx
type: challenge
title: ansible-navigator インターフェイスの詳細
teaser: この課題では、[`ansible-navigator`](https://github.com/ansible/ansible-navigator) の詳細を確認します。
  ユーザーインターフェイス
注記:
- type: text
  コンテンツ: |-
    # *ansible-navigator* インターフェイス
    <br><br>
    ### 開発者エクスペリエンスの向上
    --------
    [`ansible-navigator`](https://github.com/ansible/ansible-navigator) は、クリエイターの開発とテストのエクスペリエンスを向上させるコンテキスト認識型のユーザーインターフェイスを提供します。Ansible ドキュメント、IDE (VScode など) との統合、および自動化を作成するためのより規範的なアプローチを提供します
    <br><br>
    ## 強化されたナビゲーション
    ---------------
    [`ansible-navigator`](https://github.com/ansible/ansible-navigator) を使用すると、プレイブックの出力を簡単にナビゲートおよびフィルタリングできます。タブ:
タブ:
- title: code-server
  type: service
  hostname: code-server
  path: /editor/?folder=vscode-remote%3A%2F%2F%2fhome%2Frhel
  port: 80
難易度: 基本
制限時間: 450
---
# [`ansible-navigator`](https://github.com/ansible/ansible-navigator)
<br>

この課題では、[`ansible-navigator`](https://github.com/ansible/ansible-navigator) インターフェイスの詳細を確認し、その機能に注目します。

**1\.**まず、追加オプションなしで `ansible-navigator` を実行します。
```
ansible-navigator
```

`ansible-navigator` TUI に入ったので、ローカル環境の開発、テスト、検査に役立つ多くのサブコマンドを使用できます。デフォルトでは、`:welcome` サブコマンドがすでに発行されており、使用可能なサブコマンドの概要が簡単に表示されます。`:help` を実行すると、詳細が表示されます。

**2\.**`ansible-navigator` で次のコマンドを発行して、ping モジュールのドキュメントを表示するためのサブコマンドを試してください。
```
:doc ping
```

`:quit` コマンドを発行して、ansible-navigtor TUI を終了できます。

**3\.**簡単な Playbook を再度実行して localhost に ping しますが、今回は `-m stdout` オプションをオフにします。
```
ansible-navigator run ./test.yml
```
また、プレイブックへのパスを指定して run コマンドを発行するだけで、ansible-navigator TUI 内からプレイブックを実行することもできます: `:run ./test.yml`

一般に、`ansible-navigator` は、数字キーを使用してオプションを選択し、<kbd>Esc</kbd> キーを使用して前の画面に移動することによって行われます。

**4\.**その行に対応する番号を押して、実行されたプレイを調べます。そのプレイの一部として実行されたタスクのリストを含む次の画面に移動する必要があります。対応する行の番号を押して、タスクを調べます。

***
*9 より大きい数の行を選択する方法を知りたいですか?*数字の先頭にコロンを付けるだけです。例: 15 行目を選択するには、コマンド `:15` を発行します。
***

**5\.**<kbd>0</kbd> を押して gather_facts タスクを選択し、サブコマンド `:doc` を発行します

`ansible-navigator` の使用は、Playbook のデバッグ中に特定のタスクのドキュメントをすばやく参照するのに非常に役立ちます。

**6\.**最後に、サブコマンドをコマンドラインで `ansible-navigator` に直接渡すことができます。`セットアップ` モジュールでドキュメントを取得してみてください:
```
ansible-navigator doc setup
```

<br>

***
`ansible-navigator` で停止すると、<kbd>Esc</kbd> は常に前の画面に移動します。残っている画面がなくなったときに <kbd>Esc</kbd> を押すと、`ansible-navigator` が終了します。