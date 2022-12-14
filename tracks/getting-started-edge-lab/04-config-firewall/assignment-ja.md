---
slug: config-firewall
id: 0c5n3czzntyq
type: challenge
title: エッジファイアウォールの設定
teaser: 監視ソフトウェアをインストールしましたが、アクセスできません。WebUI にアクセスできるように､
  エッジファイアウォールを設定します。
注記:
- type: text
  コンテンツ: # 第 3 のミッション: ダブリンの拠点では、監視用ダッシュボードにアクセスする必要があります。
    \\n##### 監視ダッシュボード \\U0001F4CA はデプロイされていますが、
    トラフィックは制限されています \\U0001F6AB。\\n#####
    この課題では、必要なトラフィックのみを許可するようにファイアウォールルールを設定します。\\U0001F50E✅
     Start ボタンをクリックして､自動化を使用してこの課題を解決します｡\\n<style type="text/css"
    rel="stylesheet">\\nh1,h2{\\n  text-align: center;\\n}\\np {\\n  text-align: center;\\n}\\nimg
    {\\n  display: block;\\n  margin-left: auto;\\n  margin-right: auto;\\n  height: 60%;\\n\\n}\\n</style>"
タブ:
- title: コントローラー
  type: service
  hostname: controller-edge-lab
  port: 443
- title: Dublin アプリケーション
  type: service
  hostname: dublin-edge-lab
  path: /web/login
  port: 8088
  new_window: true
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

>**Ignition ユーザー名**:
> ```yaml
>admin
>```
>**Ignition パスワード**:
>```yaml
>learn_ansible
>```
👋 はじめに
===

### 3 番目のミッション: ダブリン工場への監視ダッシュボードへのアクセスを許可するようにファイアウォールルールを設定する
この課題では、対応するインスタンスグループを使用して、単一のリモートロケーションのファイアウォール設定を自動化する方法を確認します。

##### ⏰ 推定所要時間: *10 分*

>**❗️注意**
>
>* 必要な場合は、_Controller_ タブから提供された認証情報を使用して自動化コントローラーにログインします。
>* イメージをクリックして詳しく見ると、イメージを拡張することができます。
>* 以下は、この例で使用されている Playbook への [リンク](https://github.com/craig-br/instruqt-track-content/blob/65e9c23585f22e0c725108c1277a4c524bf58513/getting-started-edge-lab/playbooks/configure_firewall.yml) です。

☑️ タスク - ファイアウォールルールをリモートロケーションに設定する
===

##### ✏️ **automation controller** で *Configure edge firewalls* ジョブテンプレートを参照してください。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Configure edge firewalls` ドロップダウン矢印をクリックします。

<a href="#config_fw_template">
  <img alt="エッジファイアウォールの設定" src="../assets/img/config_fw_template.png" />
</a>

<a href="#" class="lightbox" id="config_fw_template">
  <img alt="エッジファイアウォールの設定" src="../assets/img/config_fw_template.png" />
</a>

`Configure edge firewalls` ジョブテンプレートは、起動時に他のインベントリーが指定されていない場合、デフォルトで `Dublin region` インベントリーを使用します。`dublin-edge-lab` 実行ノードは `Dublin region` のインベントリーに関連付けられており、ジョブテンプレートを実行します。

<a href="#config_fw_template_dublin">
  <img alt="エッジファイアウォールインベントリーの設定" src="../assets/img/config_fw_template_dublin.png" />
</a>

<a href="#" class="lightbox" id="config_fw_template_dublin">
  <img alt="エッジファイアウォールインベントリーの設定" src="../assets/img/config_fw_template_dublin.png" />
</a>

##### ✏️ *Configure edge firewalls* ジョブテンプレートを起動します。

* **Resources** セクションの下のサイドナビゲーションで、**Templates** をクリックします。
* `Configure edge firewalls` <img src="https://github.com/IPvSean/pictures_for_github/blob/master/launch_job.png?raw=true" style="width:4%; display:inline-block; vertical-align: middle;" /> アイコンをクリックして､テンプレートを起動します｡
* デフォルトの `Dublin region` を選択したままにして、`Next` をクリックします。
<a href="#Configure edge firewalls template region prompt">
  <img alt="Configure edge firewalls テンプレート region プロンプト" src="../assets/img/config_fw_template_prompt.png" />
</a>

<a href="#" class="lightbox" id="Configure edge firewalls template region prompt">
  <img alt="Configure edge firewalls テンプレート region プロンプト" src="../assets/img/config_fw_template_prompt.png" />
</a>

* `Launch` をクリックして、自動化ジョブをトリガーします。

<a href="#Launch Configure edge firewalls template">
  <img alt="Launch Configure edge firewalls template" src="../assets/img/config_fw_template_launch.png" />
</a>

<a href="#" class="lightbox" id="Launch Configure edge firewalls template">
  <img alt=" Configure edge firewalls テンプレートを起動" src="../assets/img/config_fw_template_launch.png" />
</a>

>ℹ️ `Configure edge firewalls` テンプレートは、監視アプリケーションへのトラフィックを許可するようにファイアウォールを設定します。**Jobs** 内の **Views** セクションで実行されたタスクを確認します。

<a href="#View Configure edge firewalls template job execution">
  <img alt="Configure edge firewalls テンプレートジョブ実行を表示" src="../assets/img/config_fw_template_job.png" />
</a>

<a href="#" class="lightbox" id="View Configure edge firewalls template job execution">
  <img alt="Configure edge firewalls テンプレートジョブ実行を表示" src="../assets/img/config_fw_template_job.png" />
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

* Monitoring ダッシュボードが使用可能になっていることがわかります。対応する認証情報でログインします。

<a href="#Monitoring dashboards">
  <img alt="Monitoring ダッシュボード" src="../assets/img/mondash-user.png" />
</a>

<a href="#" class="lightbox" id="Monitoring dashboards">
  <img alt="Monitoring ダッシュボード" src="../assets/img/mondash-user.png" />
</a>

* monitoring ダッシュボードには、トラフィック使用率を含む RHEL 統計が表示されます。

<a href="#Monitoring dashboards KPIs">
  <img alt="Monitoring ダッシュボードの KPI" src="../assets/img/mondash-traffic.png" />
</a>

<a href="#" class="lightbox" id="Monitoring dashboards KPIs">
  <img alt="Monitoring ダッシュボードの KPI" src="../assets/img/mondash-traffic.png" />
</a>

✅ 次の課題に進む
===
タスクを完了したら、下の `Next` ボタンを押して次のチャレンジに進みます。

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