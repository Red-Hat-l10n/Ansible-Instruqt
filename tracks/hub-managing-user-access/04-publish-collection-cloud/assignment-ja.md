---
slug: publish-collection-cloud
id: fuyq5dygaknu
type: challenge
title: クラウド自動化開発者として Private Automation Hub にコレクションを公開
teaser: このチャレンジでは、クラウド自動化グループのユーザーが、Private Automation Hub のクラウド名前空間にのみ公開する方法を説明します。
  
タブ:
- title: automationhub-terminal
  type: terminal
  hostname: privatehub-01
- title: automationhub-web
  type: service
  hostname: privatehub-01
  path: /
  port: 443
難易度: 基本
制限時間: 400
---

🔐 ログイン認証情報

>ユーザー: marie<p>
>パスワード: learn_ansible

このチャレンジは、前のチャレンジで設定されたポリシーに対して作業を行います。以下はその要約です。
1. ユーザー `marie` は、Private Automation Hub のクラウド名前空間にのみ公開できます。
2. チャレンジ 1 で説明されているとおり、ポリシーは `/etc/galaxy/galaxy-importer.cfg` でタグ付けされたコレクションのみ許可するように設定されています。

Cloud Automation グループユーザー `marie` のトークンを含む `ansible.cfg` が提供されており、学習者は `marie` ユーザーとしてコレクションを Private Automation Hub にプッシュします。

また、コレクションをプッシュしようとした場合にポリシーがどのように機能するかを示すために、いくつかのコレクションアーティファクトも含まれています。

**注記**: このラボは、`ansible-galaxy` を使用したコレクションのビルドに対応していません。Ansible コンテンツコレクションのビルド方法については、Ansible ドキュメントの [コンテンツコレクションの開発] (https://docs.ansible.com/ansible/latest/dev_guide/developing_collections.html) および [コレクション Galaxy メタデータ構造] (https://docs.ansible.com/ansible/latest/dev_guide/collections_galaxy_meta.html#collections-galaxy-meta) のページを参照してください。

☑️ タスク 1 - コレクションをネットワーク名前空間にプッシュする
===

このタスクでは、Cloud Automation グループのユーザー `marie` がコレクションを `network` 名前空間に公開します。
以前のチャレンジで設定したポリシーからも分かるとおり、**Cloud Automation** グループのユーザーはコレクションを **cloud** 名前空間にのみ公開できます。コレクションを **network** 名前空間に公開すると失敗するか確認してみましょう。

**automationhub-terminal** タブで以下のコマンドを実行します。
```
ansible-galaxy collection publish network-test_collection-1.0.0.tar.gz
```
次のエラーが表示されます:
`このアクションを実行するパーミッションがありません。`

以前の演習で、**Cloud Automation** グループのユーザーは ** cloud** 名前空間にしかコレクションを公開できないようにポリシーを設定しているため、これは意図的なものです。

☑️ タスク 2 - コレクションを cloud 名前空間にプッシュする
===
次に、**cloud** 名前空間にコレクションを公開してみましょう。**Cloud Automation** グループのユーザーとして、コレクションを Private Automation Hub の **cloud** 名前空間に発行できるはずです。

以下のコマンドを実行します。

```
ansible-galaxy collection publish cloud-lab_collection_without_tags-1.0.0.tar.gz
```

上記のコレクションの名前から、このコレクションにはタグがないことが分かります。つまり、これはポリシーに基づき失敗するはずです。

このコレクションのコレクションメタデータ (`galaxy.yml`) にタグは含まれません。
```
tags: []
```

上記のコマンドを実行すると、以下のエラーが表示されます。

`ERROR!Galaxy import process failed: Invalid collection metadata.At least one tag required from tag list: application, cloud, database, infrastructure, linux, monitoring, networking, security, storage, tools, windows (Code: UNKNOWN)`


次に下記のコマンドを実行し、タグ付きコレクションをプッシュします。このコマンドは成功するはずです。

```
ansible-galaxy collection publish cloud-lab_collection_with_tags-1.0.0.tar.gz
```
このコレクションのコレクションメタデータ (`galaxy.yml`) には、クラウドコレクションであることを示す `cloud` というタグが付けられています。
```
tags: [cloud]
```

☑️ タスク 3 - Automation Hub のインポートを確認する
===
`automationhub-web` タブでユーザー `marie` としてログインします。

🔐 ログイン認証情報

>ユーザー: marie<p>
>パスワード: learn_ansible

Cloud Automation グループのユーザーとして、名前空間に公開したコレクションを Private Automation Hub UI で確認できるようになりました。

**注記** Curator グループのユーザーの場合、まずコレクションを承認しなければ名前空間の下に直接表示されないため、ここでコレクションは名前空間の下に直接表示されません。

次のスクリーンショットでは、実行したインポートを確認する方法と、インポートに割り当てられているログを確認します。

**ラボの automationhub-web タブでユーザー marie としてログインします**

<!-- ![Cloud collection view](../assets/cloud_collection_view.png
) -->
<a href="#cloud_collection_view">
  <img alt="Cloud コレクションビュー" src="../assets/cloud_collection_view.png" />
</a>
<a href="#" class="lightbox" id="cloud_collection_view">
  <img alt="Cloud コレクションビュー" src="../assets/cloud_collection_view.png" />
</a>

<!-- ![Collection Import Button](../assets/collection_import_button.png
) -->
<a href="#collection_import_button">
  <img alt="Collection Import ボタン" src="../assets/collection_import_button.png" />
</a>
<a href="#" class="lightbox" id="collection_import_button">
  <img alt="collection import ボタン" src="../assets/collection_import_button.png" />
</a>

<!-- ![Cloud collection Import View](../assets/cloud_collection_import_view.png
) -->
<a href="#cloud_collection_import_view">
  <img alt="Cloud コレクションの Import ビュー" src="../assets/cloud_collection_import_view.png" />
</a>
<a href="#" class="lightbox" id="cloud_collection_import_view">
  <img alt="Cloud コレクションの Import ビュー" src="../assets/cloud_collection_import_view.png" />
</a>

☑️ タスク 4 - ユーザー marie としてログアウトする
===
* 次のチャレンジに進む前に、必ずユーザー marie からログアウトしてください。

☑️ まとめ
===
* Cloud Automation グループのユーザーが、コレクションをネットワーク名前空間に公開できるかテストしました。
* インポーターに対してキュレーターが設定したポリシーが、タグの有無にかかわらず機能するかどうか確認しました。
* Cloud Automation グループのユーザーとしてインポートを確認し、ステータスが Waiting for Approval となっていることを確認しました。これは、公開前にキュレーターがコレクションを承認する必要があることを示しています。

✅ 次のチャレンジ
===
タスクを完了したら、下の `Next` ボタンを押して次のチャレンジに進みます。

🐛 問題が発生しましたか?
====
問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] (https://github.com/ansible/instruqt/issues/new) してください。

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