---
slug: ansible-navigator-using-execution-environments
id: dilqtnpyq0ye
type: challenge
title: 実行環境の使用
teaser: 実行環境を使用するようにナビゲーターを設定する
注記:
- type: text
  コンテンツ: |-
    ローカルワークステーションで作成した Playbook を共有するとき、これらの Playbook を実行するチームメイトに依存関係 (コレクション、ロール、モジュール、python パッケージ、システムパッケージなど) をどのように伝えますか?

    これが実行環境の出番です!実行環境イメージは、必要なすべての依存関係を簡単に共有できるコンテナーイメージにバンドルし、自動化がどこでも確実に実行されるようにします。

    Ansible Navigator は、これらの実行環境をユーザーが作成した Playbook と一緒に使用するように構築されています。
タブ:
- title: code-server
  type: service
  hostname: code-server
  path: /editor/?folder=vscode-remote%3A%2F%2F%2fhome%2Frhel
  port: 80
難易度: 基本
制限時間: 450
---
この時点まで、`ansible-navigator` は組み込みモジュールのみで実行され、実行環境なしで実行されていました。

`ansible-navigator.yml` を変更してデフォルトの実行環境を使用するとどうなるか見てみましょう。

**1\.**`ansible-navigator.yml` を開き、`実行環境` 設定ブロックの下で enabled `: false` を `enabled: true` に変更します。ファイルは以下のようになります。
```
---
ansible-navigator:
  execution-environment:
    container-engine: podman
    image: ee-supported-rhel8:2.0.0
    enabled: true
    pull-policy: never

  playbook-artifact:
    save-as: /home/rhel/playbook-artifacts/{playbook_name}-artifact-{ts_utc}.json

  logging:
    level: debug

  editor:
    command: code-server {filename}
    console false
```

**2\.**テスト Playbook を再実行します。
```
ansible-navigator run ./test.yml
```

`ansible-navigator` は、実行環境を使用する必要があることを認識していますが、現在存在していないことに注意してください。コンテナーレジストリーから実行環境がプルされているプルプロセスが発生していることがわかります。`ansible-navigator` は、同じ yaml ファイルで設定でき、独自の Private Automation Hub からプルできます。

**3\.**`test.yml` ファイルが正常に実行されているはずです。`ansible-navigator` を使用して、`:collections` サブコマンドを発行することで、この実行環境を検証できるようになりました。

**4\.**コレクションの検証中に、`ansible.utils` コレクションには `fact_diff` と呼ばれるモジュールがあります。このモジュールの作成者を見つけ、この人に関連する github ハンドルを覚えておいてください。