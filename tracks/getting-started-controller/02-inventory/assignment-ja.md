---
slug: inventory
id: w69by5ntbgo0
type: challenge
title: インベントリーの作成
teaser: インベントリーを見ていきます。
注記:
- type: text
  コンテンツ: "# インベントリー\\n<br>\\n<p align="center">\\n  <img width="700px" src="https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inventory.png">\\n</p>\\n<br>\\n\\nAn
    [**インベントリー**](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html)
    は、ジョブを起動できるホストのコレクションです(Ansible インベントリーファイルと同様)。
    \\n\\n<style type="text/css" rel="stylesheet">\\nh1 {\\n\\ttext-align:
    center\\n\\t}\\n</style>\\n"
- type: text
  コンテンツ: "# インベントリー\\n<br>\\n<p align="center">\\n  <img width="700px" src="https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-hosts.png">\\n</p>\\n<br>\\n\\n[**インベントリー**](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html#inventory-plugins)
    はグループに分割され、これらのグループには実際のホストが含まれます。グループは、
    ホスト名をコントローラーに入力するか、サポート対象のクラウドプロバイダーから入力して、手動で読み込むことができます。
    \\n\\n<style type="text/css" rel="stylesheet">\\nh1 {\\n\\ttext-align:
    center\\n\\t}\\n</style>"
タブ:
- title: コントローラーダッシュボード
  type: service
  hostname: controller
  port: 443
- title: Controller CLI
  type: terminal
  hostname: controller
- title: Host 01 CLI
  type: terminal
  hostname: host01
- title: Host 02 CLI
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
## コントローラーダッシュボードに以下を作成します。

*ログイン認証情報:*<p>
ユーザー: admin <p>
パスワード: ansible123!

> **注記:**<p>
>
> すべてのフィールドで **大文字と小文字** が区別されるため、チェックは失敗します。割り当てで使用されているものと同じ大文字を使用していることを確認してください。

自動化コントローラーインスタンスに加えて、サンドボックス環境には、`host01` と `host02` の 2 つの仮想マシンも含まれています。

また、これらのマシンには追加のターミナルタブが追加されているので、見て回ることができます。

これらのマシンは、ssh キーを使用して相互に `ssh` できるように設定されています。

## 課題

すべてのタスクは、自動化コントローラーのダッシュボードで実行されます
* **Resources** セクションの下のサイドナビゲーションで、**Inventories** をクリックします
* **Inventories** の下で、**Add** をクリックします
* `Lab-Inventory` 
![インベントリー](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inventory.png) と呼ばれる新しいインベントリーを作成します。
***
<br>

* `Lab-Inventory` を作成したら、**Hosts** をクリックします。
* 2 つのホスト (`host01` と `host02`) を `Lab-Inventory`
![ホスト](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-hosts.png) に追加します。
***
<br>

* `host01` と `host02` を `Lab-Inventory` に追加したら、Inventory リストに戻ります。
* `Lab-Inventory` をクリックし、トップメニューで **Groups** を選択します。
* `Lab-Inventory` に `web` という新しいグループ
![group](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-add-group.png) を作成します。
***
<br>

* 新しく作成した `Web` グループをクリックし、トップメニューの **Hosts** をクリックします。
* 既存の `host01` と `host02` を `Web` グループ 
![group](https://raw.githubusercontent.com/craig-br/instruqt-tracks/devel/assets/controller/controller-inst-add-hosts-group.png) に追加します。
***
<br>

**完了したら、下の Check ボタンを押して、次のチャレンジに移動します。**