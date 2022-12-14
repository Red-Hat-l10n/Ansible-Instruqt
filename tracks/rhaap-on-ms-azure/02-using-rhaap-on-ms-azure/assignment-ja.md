---
slug: using-rhaap-on-ms-azure
id: mafsch75wznz
type: challenge
title: Microsoft Azure での Red Hat Ansible Automation Platform の使用
注記:
- type: text
  contents: |
    # 課題の概要

    この課題では、Azure 環境内のリソースに対して自動化を実行します。
    以下を実行するために、`いくつかのジョブテンプレート` を起動します。
    - Azure リソースグループを作成する
        - Azure で作成されていることを確認する
    - Windows 2022 サーバーおよび関連するすべてのリソースを作成する
        - リソースが Azure で作成されていることを確認する
    - Azure リソースグループを削除してクリーンアップを実行する
タブ:
- title: Ansible Automation Controller
  type: service
  hostname: controller
  port: 443
- title: Azure Portal
  type: website
  url: https://portal.azure.com/#home
  new_window: true
- title: Azure Portal アカウント
  type: service
  hostname: azurecloudclient
  port: 80
難易度: 基本
制限時間: 900
---
## 課題
### *所要時間: 15 分*

> Ansible Automation Platform を介して Azure リソースをデプロイします。
---

`Ansible Automation Controller` にログインします。
- `Ansible Automation Controller` タブを選択します。ラボツールバーには、多くのタブが表示されます。
![ラボタブ](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/lab-tabs.jpg)

以下の認証情報を使用してログインします。<br>
*ログイン認証情報:*<p>
`User:  admin`<p>
`Password:  ansible123!`<p>

<br><br>
---

`Azure ポータル`にログインします。
- ラボツールバーから `Azure ポータル` タブを選択します。
![ラボタブ](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/lab-tabs.jpg)

これにより、新しいブラウザータブが起動します。 `Azure Portal Account` タブから Azure 認証情報の `Email` & `Password` をコピーし、Azure ポータルにログインします。<br />

---

Automation Controller UI
* `Resources` 左メニューをデプロイメントし、`Template` を選択します
* `Create Azure Resource Group` ジョブテンプレートを選択して `Launch` をクリックするか、単に `Rocket Launcher` アイコンをクリックして起動します。
![起動アイコン](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/launch-icon.png)

* ジョブの進捗を監視します。 完了したら、次のステップに進んでください。 *これが完了するまでに数分かかります。*

Azure ポータル
* Azure でリソースグループが作成されたことを確認します。 `azure-demo` リソースグループを検索して選択し、デプロイメントします。 現在、このリソースグループ内には他のリソースがないことに注意してください。Azure portal では、ツールバーの `Refresh` アイコンを頻繁にクリックしてリストビューを更新する必要があります。

Automation Controller UI
* `Create Windows Server 2022 VM` ジョブテンプレートを選択して `Launch` をクリックするか、単に `ロケットランチャー` アイコンをクリックして起動します。

* このジョブテンプレートは、Windows 2022 Server を作成する前に必要な多数の Azure リソースの作成を調整および自動化します。 ジョブの進捗を監視します。 完了したら、次のステップに進んでください。 *これが完了するまでに数分かかります。*

Azure ポータル
* `azure-demo` リソースグループを検索して選択し、デプロイメントします。 これで、Windows 2022 サーバーに加えて作成された多くのリソースが表示されます。 この 1 つのテンプレートによって、すべてのリソースの作成が調整されました。 Azure portal では、ツールバーの `Refresh` アイコンを頻繁にクリックしてリストビューを更新する必要があります。

Automation Controller UI
* `Destroy Azure Resource Group` ジョブテンプレートを選択して `Launch` をクリックするか、単に `Rocket Launcher` アイコンをクリックして起動します。 これにより、リソースグループとその中のすべてのリソースが削除されます。 ジョブの進捗を監視します。 *これが完了するまでに数分かかります。*

Azure ポータル
* `azure-demo` リソースグループが存在しないことを確認します。 Azure portal では、ツールバーの `Refresh` アイコンを頻繁にクリックしてリストビューを更新する必要があります。

完了したら､`次の課題に進んで、` Azure リソースの自動化を実行してください。`Next` をクリックします。