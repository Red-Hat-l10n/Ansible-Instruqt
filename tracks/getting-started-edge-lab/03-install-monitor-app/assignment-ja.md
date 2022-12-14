---
slug: install-monitor-app
id: 7m0385aw639q
type: challenge
title: エッジネットワークトラフィックの監視
teaser: 次に、ダブリンとヨハネスブルグのデバイスに監視ソフトウェアをインストールします。
注記:
- type: text
  コンテンツ: "# 2 番目のミッション: ダブリンの現場は監視が必要です。\\n##### あなたは
    ローリーに拠点を置き、RHEL 監視 \\U0001F50E アプリケーションをデプロイメントする任務を負っています。
     \\n##### 接続性は貴重なリソースであり、トラフィック統計を監視し､
    \\U0001F4CA 帯域幅使用率を把握することは不可欠です｡\\U0001F4C8.\\n#####
    あなたの使命は、\\U0001F94B を受け入れることを選択した場合、
    IT パフォーマンスを監視する｢目｣ \\U0001F440 をダブリン工場にデプロイすることです。\\n##### Start ボタンをクリックして開始します。.\\n<style
    type="text/css" rel="stylesheet">\\nh1,h2{\\n  text-align: center;\\n}\\np {¨\\n
    \\ text-align: center;\\n}\\nimg {\\n  display: block;\\n  margin-left: auto;\\n  margin-right:
    auto;\\n  height: 60%;\\n\\n}\\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: controller-edge-lab
  port: 443
- title: Dublin mon
  type: service
  hostname: dublin-edge-lab
  path: /network
  port: 9090
  url: https://dublin-edge-lab:9090
  new_window: true
難易度: 基本
時間制限: 600
---

🔐 ミッションのログイン認証情報
===

>**コントローラーおよびモニターリングのユーザー名**:
> ```yaml
>student
>```
>**コントローラーおよびモニターリングパスワード**:
>```yaml
>learn_ansible
>```

👋 はじめに
===

### 2 番目のミッション: 監視ダッシュボードをダブリン工場にデプロイメントする
この課題では、対応するインスタンスグループを使用して、モニタリングダッシュボードアプリケーションを単一のリモートロケーションにデプロイする方法を確認します。

##### ⏰ 推定所要時間: *10 分*

>**❗️注意**
>
>* 必要な場合は、_Controller_ タブから提供された認証情報を使用して自動化コントローラーにログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。
>* 以下は、この例で使用されている Playbook への [リンク](https://github.com/craig-br/instruqt-track-content/blob/65e9c23585f22e0c725108c1277a4c524bf58513/getting-started-edge-lab/playbooks/deploy_monitoring.yml) です。

☑️ タスク - モニタリングダッシュボードジョブテンプレートのデプロイ
===

##### ✏️ **Automation controller** で *Deploy monitoring dashboards* ジョブテンプレートをデプロイメントするを参照してください。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Deploy monitoring dashboards` ドロップダウン矢印をクリックします。

<a href="#deploy_mondash_template">
  <img alt="監視ダッシュボードをデプロイする" src="../assets/img/deploy_mondash_template.png" />
</a>

<a href="#" class="lightbox" id="deploy_mondash_template">
  <img alt="監視ダッシュボードをデプロイする" src="../assets/img/deploy_mondash_template.png" />
</a>

`Deploy monitoring dashboards` ジョブテンプレートは、デフォルトで `Dublin region` のインベントリーを使用します。`dublin-edge-lab` 実行ノードは、`Dublin region` インベントリーに関連付けられ、ジョブテンプレートを実行します。

<a href="#deploy_mondash_template_dublin">
  <img alt="モニタリングダッシュボードインベントリーをデプロイメントする" src="../assets/img/deploy_mondash_template_dublin.png" />
</a>

<a href="#" class="lightbox" id="deploy_mondash_template_dublin">
  <img alt="モニタリングダッシュボードインベントリーをデプロイメントする" src="../assets/img/deploy_mondash_template_dublin.png" />
</a>

##### ✏️ *Deploy monitoring dashboards* ジョブテンプレートを起動します。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Deploy monitoring dashboards` <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックしてテンプレートを起動します。
* インベントリープロンプトでデフォルトの `Dublin region` を選択したままにして、`Next` ボタンをクリックします。
<a href="#Deploy monitoring dashboards template region prompt">
  <img alt="モニタリングダッシュボードテンプレートリージョンプロンプトのデプロイ" src="../assets/img/deploy_mondash_template_prompt.png" />
</a>

<a href="#" class="lightbox" id="Deploy monitoring dashboards template region prompt">
  <img alt="モニタリングダッシュボードテンプレートリージョンプロンプトのデプロイ" src="../assets/img/deploy_mondash_template_prompt.png" />
</a>

* `Launch` ボタンをクリックして、自動化ジョブをトリガーします。

<a href="#Launch Deploy monitoring dashboards template">
  <img alt="デプロイモニターリングダッシュボードテンプレートの起動" src="../assets/img/deploy_mondash_template_launch.png" />
</a>

<a href="#" class="lightbox" id="Launch Deploy monitoring dashboards template">
  <img alt="デプロイモニターリングダッシュボードテンプレートの起動" src="../assets/img/deploy_mondash_template_launch.png" />
</a>

>ℹ️ `Deploy monitoring dashboards テンプレート` は、情報収集、テンプレート作成、コンテナーイメージのプル、サービスの再起動など、複数のタスクを実行します。**Jobs** 内の **Views** セクションで実行されたすべてのタスクを確認します。

<a href="#View Deploy monitoring dashboards template job execution">
  <img alt="モニタリングダッシュボードテンプレートジョブ実行のデプロイの表示" src="../assets/img/deploy_mondash_template_job.png" />
</a>

<a href="#" class="lightbox" id="View Deploy monitoring dashboards template job execution">
  <img alt="モニタリングダッシュボードテンプレートジョブ実行のデプロイの表示" src="../assets/img/deploy_mondash_template_job.png" />
</a>


☑️ 最終タスク - Dublin 監視ダッシュボードにログインする
===
* `Dublin mon` タブをクリックして、monitoring ダッシュボードにログインしてください。

<a href="#Dublin monitoring tab">
  <img alt="Dublin monitoring タブ" src="../assets/img/dublin-mon-tab.png" />
</a>

<a href="#" class="lightbox" id="Dublin monitoring tab">
  <img alt="Dublin monitoring タブ" src="../assets/img/dublin-mon-tab.png" />
</a>

* Dublin 監視ダッシュボードは利用できません!いくつかの障害を見つけた後、チームは、新しい監視アプリケーション用にエッジファイアウォールを設定する必要があることに気付きました。
これは、次の課題で設定します。

<a href="#Service not ready yet">
  <img alt="サービスはまだ準備ができていません" src="../assets/img/pleasewait.png" />
</a>

<a href="#" class="lightbox" id="Service not ready yet">
  <img alt="サービスはまだ準備ができていません" src="../assets/img/pleasewait.png" />
</a>

✅ チャレンジをチェック
===
以下の `Check` ボタンを押して、タスクが完了したら次のチャレンジに移動します。

NORMAL で問題が発生していますか ?
====
問題が発生した場合や、何かがおかしいと気付いた場合は、[チケットを作成](https://github.com/ansible/instruqt/issues/new?labels=getting-started-edge-lab&title=Getting+started+with+Ansible+Automation+Platform+and+edge+issue:+incident-creation&assignees=dafmendo) してください。

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