---
slug: publishing-collections-with-ansible-galaxy
id: evr2at4neqer
type: challenge
title: Ansible Ansible Content Collections を Private Automation Hub インスタンスに発行します。
teaser:この課題では、コレクション tarball を Private Automation
   Hub インスタンスにパブリッシュします。
注記:
- type: text
  コンテンツ: '#### Ansible Content Collections を Private Automation Hub インスタンスに **パブリッシュ** する
    
タブ:
- title: automationhub-terminal
  type: terminal
  hostname: privatehub-01
難易度: 基本
制限時間: 300
---
この課題では、2 つのコレクション `ansible.test_collection` と `community.lab_collection` を Private Automation Hub インスタンスに発行します。

## 1\.`ansible.test_collection` を公開します。ターミナルウィンドウから次のコマンドを実行します。
```
ansible-galaxy collection publish ansible-test_collection-1.0.0.tar.gz -c
```
***

## 2\.`community.lab_collection` を Private Automation Hub インスタンスに公開します。ターミナルウィンドウから次のコマンドを実行します。

```
ansible-galaxy collection publish community-lab_collection-1.0.0.tar.gz -c
```
***

   *注記*:`-c` オプションは、SSL 証明書エラーを無視するために使用されます。

## 次の課題の **Check** をクリックします