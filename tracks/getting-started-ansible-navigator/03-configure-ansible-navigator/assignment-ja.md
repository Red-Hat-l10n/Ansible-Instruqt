---
slug: configure-ansible-navigator
id: hggv2ubzmllg
type: challenge
title: 一般的な ansible-navigator オプションの設定
teaser: 一般的なナビゲーター設定を見てみましょう。
注記:
- type: text
  コンテンツ: |-
    `ansible-navigator` は、開発エクスペリエンスを統一する方法として導入されました。このため、開発者/プロジェクトごとにカスタマイズできる設定ディレクティブが多数あります。

    `ansible-navigator.yml` は、`ansible-navigator` で自動化を作成および実行する方法を決定する、各プロジェクトに存在する設定ファイルです

    これらのオプションのいくつかを見てみましょう。
タブ:
- title: code-server
  type: service
  hostname: code-server
  path: /editor/?folder=vscode-remote%3A%2F%2F%2fhome%2Frhel
  port: 80
難易度: 基本
制限時間: 450
---
`ansible-navigator` には独自の設定があり、プロジェクトごとに設定できます。これは、プロジェクトが複数の実行環境にまたがる場合や、異なる ansible デフォルトが必要な場合などに役立ちます。

さらに、開発者はこれらの設定を使用して、`ansible-navigator` を開発スタイル、コードエディター/IDE などに適応させることができます。

一般的なオプションのいくつかを見てみましょう。

**1\.**ディレクトリー `/home/rhel` に、`ansible-navigator.yml` というファイルが表示されます。これを開き、コンテンツを確認します。現在、いくつかの実行環境とログ設定がすでにそこにあることに注意してください。

開発者は、統合されたターミナル内で ansible-navigator を実行できるだけでなく、検査のためにタスク出力をコードエディターに戻せるようにしたいと考えています。

**2\.** `ansible-navigator` は、`:open` サブコマンドの優先エディターを設定できます。今それをしましょう。`ansible-navigator.yml` を開き、お好みのエディターを環境内の code-server インスタンスに設定します。これを行うには、次の設定をファイルの末尾にコピーします。
```

  editor:
    command: code-server {filename}
    console: false
```

**3\.**テスト Playbook を実行します。
```
ansible-navigator run ./test.yml
```

**4\.**<kbd>0</kbd> を押してプレイを調べ、もう一度 <kbd>0</kbd> を押して最初のタスクを調べ、サブコマンド `:open` を発行します。

コードエディター内に、そのタスクの出力をファイルの内容として含む新しいタブが表示されます。`:open` は、ナビゲーター TUI 内の任意のページで機能し、プレイブックの作成に役立ちます。