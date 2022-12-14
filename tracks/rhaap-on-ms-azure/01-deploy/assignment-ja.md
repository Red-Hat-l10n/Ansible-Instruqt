---
slug: deploy
id: zpumxgrfkti8
type: challenge
title: Red Hat Ansible Automation Platform を Microsoft Azure にデプロイする方法
注記:
- type: text
  コンテンツ: |-
    ラボ環境の作成がまだ開始されていない場合は、*右下隅* にある 緑の Start ボタン <img src="https://github.com/IPvSean/pictures_for_github/blob/master/start_button.png?raw=true" width="100px" align="right"> をクリックしてください にある<br />

    始める前に、Microsoft Azure での Red Hat Ansible Automation Platform の **利点** をいくつか紹介しましょう。

    ---
     `(下にスクロールしてください)`

    <p align="center">
      <img width="500px" src="https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/aap-azure-ben.jpg">
    </p>
- type: text
  コンテンツ: |-
    **Red Hat Ansible Automation Platform を Microsoft Azure** にデプロイするには、Azure Marketplace に移動し、そこから選択して、**Create** をクリックします。`(下にスクロールしてください)`

    <p align="center">
      <img width="500px" src="https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/AAP-01-AzureMarketPlace.jpg">
    </p>
- type: text
  contents: |
    デプロイ、**サブスクリプション、リソースグループ、リージョン、アプリケーション名、管理者パスワード** の詳細を入力します。

    **Access** には、**Private** または **Public** を選択します。 プライベートは、完全なプライベートネットワークで Ansible Automation Platform を Microsoft Azure にデプロイします。 Public は、アプリケーションゲートウェイとファイアウォールを使用して、Automation Controller および Private Automation Hub ユーザーインターフェイスをパブリックインターネットに公開します。

    **Next : Networking >** をクリックします。`(下にスクロールしてください)`

    <p align="center">
      <img width="700px" src="https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/AAP-02-AzureMarketPlace.jpg">
    </p>
- type: text
  contents: |
    ネットワーク設定の詳細を入力します。 これにより、Ansible Automation Platform on Microsoft Azure をデプロイするプライベートネットワークを指定できます。 これは、他の既存の内部ネットワークと混同しないネットワークであることを確認します。 **Create new** をクリックしてネットワーク情報を入力します。 完了したら、保存します。

    **Next : Review + create >** をクリックします。`(下にスクロールしてください)`

    <p align="center">
      <img width="700px" src="https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/AAP-02-2-AzureMarketPlace.jpg">
    </p>
- type: text
  contents: |
    最後に、**上記の利用規約に同意します** というタイトルのボックスをオンにして、**Co-Admin Access Permission** に同意します。

    次に、**Create** をクリックします。`(下にスクロールしてください)`

    <p align="center">
      <img width="700px" src="https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/AAP-02-3-AzureMarketPlace.jpg">
    </p>
- type: text
  コンテンツ: |-
    **作成** 後、Red Hat Ansible Automation Platform on Microsoft Azure のデプロイが続行されます。これは完了するまでに少し時間がかかります。

    デプロイメントが完了すると、マネージドアプリケーションオブジェクトが表示され、正常にデプロイメントされたことが示されます。
     `(下にスクロールしてください)`

    <p align="center">
      <img width="800px" src="https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/AAP-03-AzureMarketPlace.jpg">
    </p>
- type: text
  コンテンツ: |-
    デプロイメントが完了すると、**Parameters and Outputs** に移動します。

    **Automation Controller** および **Private Automation Hub** ユーザーインターフェイスを起動するには、URL をコピーして、選択したブラウザーで起動します。

    **Microsoft Azure で Red Hat Ansible Automation Platform** をお楽しみいただけるようになりました。`(下にスクロールしてください)`

    <p align="center">
      <img width="800px" src="https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/AAP-04-AzureMarketPlace.jpg">
    </p>
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
  path: /
  port: 80
難易度: 基本
timelimit: 300
---
## 課題
### *所要時間: 5 分*

> Red Hat Ansible Automation Platform を Microsoft Azure にデプロイする方法を簡単に説明しました。
>
> `Ansible Controller UI` および `Azure ポータル` にログインしてみましょう。
---

# Automation Contoller へのログイン<p>
- `Ansible Automation Controller` タブを選択します。ラボツールバーには、多くのタブが表示されます。
![ラボタブ](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/lab-tabs.jpg)

以下の認証情報を使用してログインします。<br>
*ログイン認証情報:*<p>
`User:  admin`<p>
`Password:  ansible123!`<p>
正常にログインできたことを確認します。
<br><br><br>
---
# Microsoft Azure ポータルにログインします<p>
- ラボツールバーから `Azure ポータル` タブを選択します。
![ラボタブ](https://raw.githubusercontent.com/ansible-cloud/azure-demos/main/images/lab-tabs.jpg)

これにより、新しいブラウザータブが起動します。 `Azure Portal Account` タブから Azure 認証情報の `Email` & `Password` をコピーし、Azure ポータルにログインします。<p>
正常にログインできたことを確認します。<p>
<br>
完了したら､`次の課題に進んで、` Azure リソースの自動化を実行してください。`Next` をクリックします。