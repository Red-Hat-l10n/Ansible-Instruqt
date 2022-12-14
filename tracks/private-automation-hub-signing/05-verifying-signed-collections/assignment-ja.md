---
slug: verifying-signed-collections
id: mchcohzehvll
type: challenge
title: ボーナス演習: ansible-galaxy CLI を使用した署名付きコンテンツコレクションの検証
  '
teaser: `ansible-galaxy` CLI を使用して、署名されたコレクションを確認しましょう
注記:
- type: text
  コンテンツ: '#### ボーナス演習: ansible-galaxy CLI を使用して ***署名されたコンテンツコレクションを検証する***
    ansible-galaxy CLI'
タブ:
- title: automationhub-terminal
  type: terminal
  hostname: privatehub-01
難易度: 基本
制限時間: 300
---
`ansible-galaxy` CLI および署名で `--keyring` オプションを使用して、Private Automation Hub インスタンスのバージョンと比較することにより、署名されたコレクションを検証することもできます。
署名されたコレクションの改ざんを試みてから、`ansible-galaxy collection verify` サブコマンドを使用して検証します。
## 1\.署名済みコレクション `community.lab_collection` に新しい空のプラグインを追加します
以下のコマンドを実行します。
```
touch ~/.ansible/collections/ansible_collections/community/lab_collection/docs/README.md
```

## 2\.改ざんされたコレクションを確認する
以下のコマンドを実行します。
```
ansible-galaxy collection verify community.lab_collection --keyring keyring.kbx -c
```
このコマンドは、コレクションのローカルバージョンと Private Automation Hub インスタンスのリモートバージョンを比較します。出力には、変更/追加/削除されたファイルが表示されます。
verbosity `-vvvv` を使用した出力は、追加の詳細を提供します
```
(exit code 0)
GnuPG signature verification succeeded, verifying contents of community.lab_collection:1.0.0
MANIFEST.json hash: f285e70041487374977afd4d1c7b917a6b15b52b340d66f513155417a8cb4e6b
Collection community.lab_collection contains modified content in the following files:
    docs/README.md
    Expected: the file does not exist
    Found: the file exists
```
***

これにより、コンテンツ署名演習の完了をマークします。**Next** をクリックして、この演習を完了します。
