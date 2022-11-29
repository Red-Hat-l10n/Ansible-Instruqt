---
slug: controller-getting-started-jt
id: l7shwh9na7oh
type: challenge
title: ジョブテンプレートの編集
teaser: この課題では、ジョブテンプレートを使用して自動化を実行します。
注記:
- type: text
  コンテンツ: "# ジョブテンプレートを使用した自動化の実行\\n<br>\\n<p align="center">\\n
    \\ <img width="700px" src="https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller_jt.png">\\n</p>\\n<br>\\n\\n[**ジョブ
    テンプレート **](https://docs.ansible.com/automation-controller/latest/html/userguide/job_templates.html)
    は、Ansible Playbook を実行するための定義およびパラメーターのセットです。\\n\\n
    コントローラーでは、ジョブテンプレートとは `ansible-playbook`
    コマンドと、コマンドラインから実行するときに使用できるすべてのフラグを視覚的に表したものです。\\n\\n<style
    type="text/css" rel="stylesheet">\\nh1 {\\n\\ttext-align: center\\n}\\n</style>"
タブ:
- title: コントローラーダッシュボード
  type: service
  hostname: controller
  port: 443
- title: Controller CLI
  type: terminal
  hostname: controller
- title: Host01 CLI
  type: terminal
  hostname: host01
- title: Host02 CLI
  type: terminal
  hostname: host02
- title: エディター
  type: service
  hostname: controller
  path: /editor/
  port: 443
難易度: 基本
制限時間: 600
---
## 課題

*ログイン認証情報:*
ユーザー: **admin**
パスワード: **ansible123!**

すべてのタスクはコントローラーダッシュボードで実行されます

* **Templates** は、
![jtmenu](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-templates-menu.png) ナビゲーションバーから開きます。
***
<br>

* `Debug-Info` ジョブテンプレート
![jtclick](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-jt-click.png) をクリックします。
***
<br>

* `Edit` 
![jtedit](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-jt-edit.png) をクリックします。
***
<br>

* いくつかのオプションを詳しく見てみましょう。
  * 以前に作成した `Lab-Inventory` を使用していることに注意してください
  * `playbooks/infrastructure/debug_info.yml` を実行します
  * SSH クレデンシャルを使用して、**host01** と **host02** を、`Lab-Inventory`
![jtexplore](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-jt-explore.png) で認証しています。
***
<br>

* **Cancel** をクリックしてから、**Launch** を押して
![inv_src](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-jt-launch.png) を起動します。
***
<br>

* この **ジョブテンプレート** は、`host01` と `host02` を持つ `Web` グループからデバッグ情報を収集します
  * 出力を見て、フィルター 
![inv_src](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-jt-output.png) を調べます。
***
<br>

**確認が終わりましたら、下のチェックボタンを押してください。お疲れさまでしたトラックを完了しました。**

<style type="text/css" rel="stylesheet">
h1 {
	text-align: center
	}
	img {
		width: 100%
	}
</style>