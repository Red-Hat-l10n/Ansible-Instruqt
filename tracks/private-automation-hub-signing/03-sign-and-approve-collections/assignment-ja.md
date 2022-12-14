---
slug: sign-and-approve-collections
id: frws8uf5aw6y
type: challenge
title: Private Automation Hub UI から Ansible Content Collections の署名および承認
  
teaser:この課題では、公開された Ansible Conent Collections に署名し、
  承認します。
注記:
- type: text
  contents: |
    #### Private Automation Hub UI から Ansible コンテンツコレクションに **署名して承認** します。
タブ:
- title: automationhub-web
  type: service
  hostname: privatehub-01
  port: 443
難易度: 基本
制限時間: 400
---
この課題では、発行された Ansible Content Collection に署名して承認します。このチャレンジで使用できる唯一のタブは、`automationhub-web` です。これは、Private Automation Hub が、署名および承認のために受信コレクションをステージングできるようになっているためです。
以下の手順を実施します。
***

## 1\.以下の認証情報を使用して、automationhub-ui タブで Private Automation Hub インスタンスにログインします。
```
Username: admin
Password: ansible123!
```
***
## 2\.ログインしたら、左側のナビゲーターペインからコレクション `> ` Approval をクリックします。

![](../assets/signing_approval.png "")
***
## 3\.前回の演習でコレクションをパブリッシュしたので、Approve ページで、プッシュした両方のコレクションの前に **Sign and approve** ボタンが表示されます。
両方のコレクションの **Sign and approve** ボタンをクリックします。
![](../assets/signing_review.png "")
***
## 4\.両方のコレクションに署名して公開したので、**Collection** ページに署名済みとして表示されます。
![](../assets/signing_collections_screen.png "")
***
## 5\.お疲れさまでした。これで、Private Automation Hub インスタンスのコレクションに署名したので、次の課題の **Check** をクリックします｡
