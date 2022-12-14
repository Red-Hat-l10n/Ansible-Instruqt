---
slug: understanding-lab-environment
id: cvorjn9mga5s
type: challenge
title: ラボ環境について
teaser: この課題では、コレクションのラボ環境設定を理解します。
  プロジェクトの署名と検証
注記:
- type: text
  コンテンツ: |-
    #### **コンテンツ署名** は、**テクノロジープレビュー** 機能として **Ansible Automation Platform 2.2** で利用可能な新しいセキュリティー中心の機能です。


    #### エンドツーエンドのコンテンツ署名と配布を目的に、Ansible 自動化コンテンツ向けの一連のケーブル用の新しいフレームワークを確立します。最初に、コレクションをデジタル署名してから、今後実行される実行環境から始めます。この機能は、エンタープライズで実行される自動化が認定され、準拠していることを確認するのに役立ちます。
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
制限時間: 300
---
課題を開始する前に、最初にラボ環境を理解することが重要です。このラボでは、2 つのタブが表示されます。

* `automationhub-terminal` \- このタブを使用して、ansible-galaxy cli からコマンドを実行して AutomationHub WebUI と対話します。
* `automationhub-web` \- これはプライベート自動化ハブの WebUI であり、アップロードされたコレクションに署名および承認するために使用されます。以下のユーザー名/パスワードの組み合わせを使用して WebUI にログインできます。
  * ユーザー名: `admin`
  * パスワード： `ansible123!`

このシステムには、Ansible Automation Platform 2.2 インストーラーから `ansible-galaxy` CLI ツールがすでにインストールされています。ターミナルタブで `ls` コマンドを実行すると、以下で説明されているアーティファクトがいくつか表示されます。

1. `ansible.cfg` \- このファイルには、インストールされたプライベート Automation Hub と対話するための Galaxy 設定が含まれています。これは、現在のフォルダ (`/home/rhel/`) から実行されるすべての` ansible-galaxy` コマンドが、このラボで展開されたプライベート・オートメーション・ハブと相互作用することも意味します。
2. `ansible-test_collection-1.0.0.tar.gz` \- プライベート Automation Hub インスタンスにプッシュされるダミーコレクション。名前空間 `ansible` はプライベート Automation Hub にすでに存在します。
3. `community-lab_collection-1.0.0.tar.gz` \- プライベート Automation Hub インスタンスにプッシュされるダミーコレクション。ネームスペース `community` はプライベート Automation Hub にすでに存在します。
4. `galaxy_signing_service.asc` \- これは、プライベート Automation Hub インスタンスでの署名を設定するために使用される gpg キーペアからの公開キーです。このキーは、プライベート Automation Hub からのコレクションのインストールと検証に使用されます。

***
コンテンツ署名検証機能は `ansible-core` バージョン >=2.13 でのみ使用できます。以下のコマンドを使用して `ansible` のバージョンを確認できます。
```
ansible --version
```
***
**Next** ボタンをクリックして学習を続行します。