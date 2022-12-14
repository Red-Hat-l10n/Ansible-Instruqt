---
slug: install-signed-collections
id: ytivx8htgeg1
type: challenge
title: 署名されたコレクションを Private Automation Hub インスタンスからインストールします。
teaser:ansible-galaxy CLI を使用して、Private Automation Hub インスタンスから署名されたコンテンツコレクション
  を取得する方法について説明します。
注記:
- type: text
  内容: '#### Private Automation Hub インスタンスから署名されたコレクションを **インストール** します。
タブ:
- title: automationhub-terminal
  type: terminal
  hostname: privatehub-01
難易度: 基本
制限時間: 500
---
Ansible Content Collections に署名してプライベート Automation Hub に公開したので、署名済みコレクションをインストールする方法と、署名機能をサポートするために `ansible-galaxy` CLI で使用できる新しい cli オプションについて学習します。

`automationhub-terminal` タブで以下の手順を行います。
***

## 1\.システム上の GPG キーリングに公開鍵を追加します。
このセクションの冒頭で、署名されたコレクションを検証してインストールするためにラボで提供される公開鍵 (`galaxy_signing_service.asc`) について少し説明しました。`ansible-galaxy` CLI で公開鍵を使用するには、システムの GPG キーリングに公開鍵を追加する必要があります。次のコマンドを実行してください。
```
gpg --import --no-default-keyring --keyring ~/keyring.kbx galaxy_signing_service.asc
```
*注:* `--no-default-keyring` オプションを削除して、デフォルトのキーリングを使用することもできます。コマンドは次のようになります。

```
gpg --import galaxy_signing_service.asc
```
上記のコマンドは、`~/.gnupg/` の場所に `pubring.kbx` というデフォルトのキーリングを作成します。この場合、キーリングは `/home/rhel/.gnupg/pubring.kbx` になります。
***
## 2\.`ansible-galaxy` CLI で `--keyring` オプションを使用せずにコレクションをインストールする
署名検証プロセスは純粋にオプトインであり、`ansible-galaxy` CLI の `--keyring` オプションを指定しない場合、コレクションのインストールは署名検証なしで行われます。
検証なしで `ansible.test_collection` をインストールすると、`ansible-galaxy` CLI が署名検証に関する警告を出力するようになることがわかります。
以下のコマンドを実行します。
```
ansible-galaxy collection install ansible.test_collection -c
```

出力には、次のような警告が表示されます。
```
[WARNING]: The GnuPG keyring used for collection signature verification was not configured but signatures were provided by the Galaxy server to verify authenticity. Configure a
keyring for ansible-galaxy to use or disable signature verification. Skipping signature verification.
```
***
## 3\.`ansible-galaxy` CLI で `--keyring` オプションを使用してコレクションをインストールする
次に、`--keyring` オプションを指定して `community.lab_collection` をインストールします。これにより、署名の検証後にコレクションが確実にインストールされます。署名の検証が行われているかどうかを確認するには、コレクションのインストールコマンドに `-vvvv` を追加する必要があります。
以下のコマンドを実行します。
```
ansible-galaxy collection install community.lab_collection --keyring /home/rhel/keyring.kbx -c -vvvv
```
*注:* 詳細出力の最後の 3 行は、署名の検証が成功したことを示しています。
```
.
.
.
(exit code 0)
GnuPG signature verification succeeded for community.lab_collection
community.lab_collection:1.0.0 was installed successfully
```
***
## 4\.コレクションインストールを含む新しいアーティファクト。
署名されたコレクションを使用すると、`ansible-galaxy` CLI は、コレクションの署名を含む `GALAXY.yml` というファイルを含む新しいディレクトリーも作成します。
`automationhub-terminal` で次のコマンドを実行します。
```
cat ~/.ansible/collections/ansible_collections/community.lab_collection-1.0.0.info/GALAXY.yml
```
これにより、コレクションの署名が含まれるファイルの内容が提供されます。
***
## 5\.お疲れさまでした。これで、プライベート Automation Hub インスタンスから署名されたコレクションがインストールされました。次の演習の **Check** をクリックします。