---
slug: playground
id: mgywzlmyzv0e
type: challenge
title: Automation Mesh プレイグラウンド
teaser: この課題でメッシュスキルをテストします。
注記:
- type: text
  コンテンツ: "# \\U0001F680 Automation Mesh プレイグラウンド\\n最後の課題では、
    このラボで学んだことを復習します。これまでの演習で学んだことを使用して、ACME Corp Automation Mesh を設定します。
    または、
    残りの時間を使って操作の確認をしてみてください。\\n\\n<style type="text/css" rel="stylesheet">\\nh1,h2{\\n
    \\ text-align: center;\\n}\\np {\\n  text-align: center;\\n}\\nimg {\\n  display: block;\\n
    \\ margin-left: auto;\\n  margin-right: auto;\\n  width: 80%;\\n}\\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: raleigh-controller
  port: 443
難易度: 基本
制限時間: 300
---
🔐 ログイン認証情報
===
すべてのログインで同じ認証情報が使用されます。

>**ユーザー名**:
> ```yaml
>student
>```
>**パスワード**:
>```yaml
>learn_ansible
>```

👋 はじめに
===

#### ⏰ 推定所要時間: 15 分

この課題では、Automation Mesh を設定します。プレイグラウンドでは、タスクの完了方法に関して、これまでのような段階的な説明を減らしています。

この課題にはチェックがないため、この環境を確認する場合は自由に行ってください。

👍 がんばってください。

>**❗️注意**
>
>* ブラウザーの左上にある _Controller_ タブで、すべてのタスクを実行します。
>* 必要な場合は、提供された認証情報を使用してAutomation Controller にログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。
>* 今回の課題のタスクチェックには、数秒かかる場合があります。
>* この演習では `Mesh route info` ジョブテンプレートを実行して、Automation Mesh が新しいピア接続をどのように作成するかを確認します。

☑️ タスク - ラボのシナリオ
===

<a href="#disconnected">
  <img alt="オフラインインストール" src="../assets/img/disconnected.png" />
</a>

<a href="#" class="lightbox" id="disconnected">
  <img alt="オフラインインストール" src="../assets/img/disconnected.png" />
</a>

現在、Johannesburg リモートオフィスにある `jhb-exec` ワーカーノードは、ACME Corp Raleigh データセンターから到達できません。セカンダリーネットワークリンクは、アイルランドにある Dublin クラウドリージョンを介して存在します。

ACME Corp の IT チームは、Johannesburg の問題のトラブルシューティングを行うには、`Debug info` ジョブテンプレートを実行する必要があります。

☑️ タスク - ラボ環境
===

ACME Corp には、Automation Controller で以下が事前に作成されています。

##### インベントリーおよび関連するホスト:

* `Johannesburg DC`.
* `Raleigh DC`.
* `Dublin DC インベントリー`

##### Automation Mesh ワーカーノード:

* `Raleigh-controller` は、Raleigh データセンターの **ハイブリッド** ノードとして設定されます。
* `jhb-exec` は、Johannesburgremoyte オフィスで **実行** ノードとして設定されます。
* `Dublin-hop` は、Dublin パブリッククラウドリージョンで **ホップ** ノードとして設定されます。

☑️ タスク - インスタンスグループおよびインベントリー
===

##### ✏️ 必要なインスタンスグループ、関連付け、およびインベントリーを作成します。

* `Raleigh data center` インスタンスグループを作成し、`raleigh-controller` インスタンスをそのインスタンスグループに関連付けます。
* `Raleigh DC` インベントリーが `Raleigh data center` インスタンスグループを使用するように設定します。
* `Johannesburg data center` インスタンスグループを作成し、`jhb-exec` インスタンスをそのインスタンスグループに関連付けます。
* `Johannesburg DC` インベントリーが `Johannesburg data center` インスタンスグループを使用するように設定します。

☑️ タスク - dublin-hop ノードの設定
===

##### ✏️ ジョブテンプレートを実行し、Dublin ホップノードを設定してテストします。

* `Setup Dublin hop node` ジョブテンプレートを実行し、`dublin-hop`ノードを有効にします。
* `Johannesburg DC` インベントリーを使用して `Debug info` ジョブテンプレートを実行します。

`Debug info` ジョブテンプレートが正常に実行されると、ミッションの完了です。

**ラボが終了しました。お疲れさまです。**

👏 ラボの終了
===

`Next` ボタンを押して、ラボを終了します。

🐛 問題が発生していますか ?
====

問題が発生した場合や、正しくない点に気付いた場合は、[チケットを作成] してください (https://github.com/ansible/instruqt/issues/new?labels=getting-started-mesh&title=Getting+started+with+automation+mesh+issue&assignees=craig-br)。

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