---
slug: devops-playground
id: 0lw2coaydkzw
type: challenge
title: プレイグラウンド
teaser: 残りの時間を使って、ご自身で試してみてください。このチャレンジはチェックされませんので、
  ご自由にいろいろと試してみて下さい。
注記:
- type: text
  コンテンツ: |-
    # チャレンジの概要
    ここはプレイグラウンドです。ご自由に試してみて、さまざまなオプションにトライしてみてください。

    ![env_tools](../assets/img/slides_5_cicd_complete.png)

    <style type="text/css" rel="stylesheet">
    h1,h2{
      text-align: center;
    }
    p {
      text-align: center;
    }
    img {
      display: block;
      margin-left: auto;
      margin-right: auto;
      width: 80%;
    }
    </style>
タブ:
- title: コントローラー
  type: service
  hostname: controller
  port: 443
- title: VS Code
  type: service
  hostname: controller
  path: /editor/?folder=/home/rhel/acme_corp
  port: 443
- title: Gitea
  type: service
  hostname: gitea
  path: /student/acme_corp
  port: 3000
- title: Jenkins
  type: service
  hostname: jenkins
  path: /job/ACMECorp/
  port: 8080
- title: Let's Quiz!
  type: service
  hostname: controller
  port: 8000
難易度: 中級
制限時間: 600
---
🔐 ログイン認証情報
===
すべてのログインで同じ認証情報が使用されます。

>ユーザー: student<p>
>パスワード: learn_ansible

👋 はじめに
===

このラボでは、自動化コントローラーのエンタープライズ機能を使用して、ACME Corp の開発チームと運用チームが共に統合および自動化する方法を強化しました。

今度はあなたの番です。

✅次の場所
===

自動化への取り組みを始めたばかりの方でも、経験豊富なベテランの方でも、自動化の知識を深めるためのさまざまなリソースを利用できます。

* [自分のペースで進められる演習](https://www.redhat.com/en/engage/redhat-ansible-automation-202108061218) - すべてが自分のペースで進められるラボをご覧ください
* [トライアルサブスクリプション](http://red.ht/try_ansible) - お使いの環境にインストールする準備はできていますか?Ansible Automation Platform のすべてのコンポーネントに無制限にアクセスするには、トライアルサブスクリプションを取得してください。
* [Red Hat Ansible Automation Platform の YouTube チャンネルにサブスクライブします。](https://www.youtube.com/ansibleautomation)

NORMAL で問題が発生していますか ?
====
ワークフロー全体を再起動する必要がある場合は、自動コントローラーで `Restart DevOps Workflow` ジョブテンプレートを実行します。

問題が発生した場合や気になる点がある場合は、[チケットを作成](https://github.com/ansible/instruqt/issues/new?labels=devops-controller&title=New+DevOps+with+automation+controller+issue+issue:+incident-creation&assignees=craig-br) してください。

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