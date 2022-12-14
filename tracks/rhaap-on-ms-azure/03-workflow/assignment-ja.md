---
slug: workflow
id: hjxsoyvqgeho
type: challenge
title: ワークフローテンプレートを使用した Azure Automation
注記:
- type: text
  コンテンツ: |-
    # 課題の概要

    `(下にスクロールしてください)`

    このチャレンジセクションでは、まず `Workflow Template` を作成して、Azure 環境内のリソースに対して自動化を実行します。

    ワークフロージョブテンプレートは、リリースプロセスの一部であったジョブの完全なセットを 1 つのユニットとして追跡するタスクを実行する一連の異なるリソースをリンクします。

    次に、ワークフローテンプレートを起動し、進行状況を監視します。

    `Workflow Template` の作成に使用する個々の `Job Templates` にタスクを分割しました。 Job Templates はすでに作成されています。

    以下を実行するための`ワークフローテンプレートを作成します`。
    - リソージグループを作成する
    - 仮想ネットワークを作成する
    - サブネットを作成する
    - パブリック IP を作成する
    - ネットワークセキュリティーグループを作成する
    - 仮想 NIC を作成する
    - 仮想マシンを作成する

    `ワークフローテンプレートを起動`します。
    - ワークフローが完了するまでの進行状況を監視する
    - Azure でリソースが作成されたことを確認する

    Azure リソースグループを削除してクリーンアップを実行する
タブ:
- title: Ansible Automation Controller
  type: service
  hostname: controller
  port: 443
- title: Azure Portal
  type: website
  hostname: azurecloudclient
  url: https://portal.azure.com/#home
  new_window: true
- title: Azure Portal アカウント
  type: service
  hostname: azurecloudclient
  port: 80
難易度: 基本
制限時間: 1500
---
## 課題
### *所要時間: 25 分*

> ワークフローテンプレートを使用した Azure Automation。
---

`Ansible Automation Controller` にログインします。
- `Ansible Automation Controller` タブを選択します。ラボツールバーには、多くのタブが表示されます。
![ラボタブ](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/lab-tabs.jpg)

以下の認証情報を使用してログインします。<br>
*ログイン認証情報:*<p>
`User:  admin`<p>
`Password:  ansible123!`<p>

<br>

`Azure ポータル`にログインします。
- ラボツールバーから `Azure ポータル` タブを選択します。
![ラボタブ](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/lab-tabs.jpg)

これにより、新しいブラウザータブが起動します。 `Azure Portal Account` タブから Azure 認証情報の `Email` & `Password` をコピーし、Azure ポータルにログインします。<br />

---
作成済みの多数の `Job Templates` をつなぎ合わせる `Workflow Template` を作成しましょう。

Automation Controller UI
* `Resources` 左メニューをデプロイメントし、`Template` を選択します
* `Add` をクリックし、ドロップダウンから `Add workflow template`を選択します。
* `Name` フィールドに `01-My Azure Automation Workflow` と入力し、一番下までスクロールして `Save` をクリックします。
* Workflow Visualizer が表示されます。 緑色の `Start` ボタンをクリックして、ワークフロータスクの定義を開始します。
  * `Add Node` ビューが表示されます。 `wf01-Create Resource Group` を選択し、`Save` をクリックします。
  * `wf01-...` にカーソルを合わせ、`+` 記号をクリックして次のノードを追加します。
  * `Run type` で `On Success` 時 が選択されていることを確認し、`Next` をクリックします。
  * `wf02-Create Virtual Network` を選択し、`Save` をクリックします。
  * 同じプロセスを繰り返し、`wf03-....` を `wf07-....` まで追加します。
  ![Workflow Visualizer](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/Workflow-image1.jpg)
  * 7 つのジョブテンプレートをすべて追加したら、`Save` をクリックしてから、`Back to Templates` をクリックしてください。
  ![Workflow Template](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/Workflow-image2.jpg)
  * `01-My Azure Automation Workflow` を選択して `Launch` をクリックするか、単に `ロケットランチャー` アイコンをクリックして起動します。
  ![起動アイコン](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/launch-icon.png)
  * ワークフロージョブの進行状況を監視します。 *これが完了するまでに数分かかります。*

**注:** ビジュアライザーでワークフローを構築しているため、`Toggle Tools` を使用してズームインおよびズームアウトする必要がある場合があります。
![Toggle Tools](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/Workflow-image3.jpg)

Azure ポータル
* `azure-demo` リソースグループを検索して選択し、デプロイメントします。 今回は、ワークフローテンプレートジョブの実行によって、リソースグループと他のすべてのリソースが作成されました。 ワークフローテンプレートの構築を活用することで、自動化の可能性は無限大になります。 Azure portal では、ツールバーの `Refresh` アイコンを頻繁にクリックしてリストビューを更新する必要があります。

Automation Controller UI
* 先に進み、作成したリソースをクリーンアップしましょう。 `Destroy Azure Resource Group` ジョブテンプレートを選択して `Launch` をクリックするか、単に `Rocket Launcher` アイコンをクリックして起動します。 これにより、リソースグループとその中のすべてのリソースが削除されます。 ジョブの進捗を監視します。 *これが完了するまでに数分かかります。*

Azure ポータル
* ワークフローによって作成されたすべてのリソースが存在しないことを確認してください。 Azure portal では、ツールバーの `Refresh` アイコンを頻繁にクリックしてリストビューを更新する必要があります。

Microsoft Azure 上の Red Hat Ansible Automation Platform について学ぶために時間を割いていただき、ありがとうございます。