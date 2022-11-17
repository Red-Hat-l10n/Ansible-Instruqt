---
slug: ahub-install
id: dvtciaf9iguk
type: challenge
title: Operator を使用した Private Automation Hub のインストール
タブ:
- title: Web コンソール
  type: website
  hostname: crc
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: ターミナル 1
  type: terminal
  hostname: crc
難易度: 基本
timelimit: 300
---
以前のチャレンジでは、AAP から自動化コントローラーコンポーネントをインストールしました。インストールが完了したら、引き続き AAP Operator の詳細ウィンドウ内からプライベート Automation Hub コンポーネントをインストールします。

## 自動化メッシュのインストール

* Operators-> `Installed Operators-> Ansible Automation Platform` Operator details ウィンドウで、`Automation Hub` というラベルのタブを選択します。

![Operator の詳細](../assets/ahub_tab.png)

* 選択したら、`Create AutomationHub` というラベルの青いボタンを選択します。
* `Create AutomationHub` ウィンドウで、プライベート Automation Hub の名前を指定します（例： `my-automation-hub` ）。`Storage Type` ドロップダウンメニューで `File` を選択します。

> **_注記：_** `Storage Type` の他のオプションは、`S3` および `Azure` などの他のオプションです。

* Form ビューの下部で、青色の `Create` ボタンをクリックします。

![AHub フォームビュー](../assets/ahub_form.png)

> **_注記：_** このデモラボでは、プライベート Automation Hub のインストールにデフォルトを使用します。Form ビューでプライベート Automation Hub を設定する以外に、YAML ビューを使用してカスタマイズしたり、Form ビューの `Advanced configuration` タブから詳細設定を設定したりできます。

* 作成が行われると、`my-automation-hub` の新規インストール用に、OpenShift リソースの多くは作成されます。

![AHub リソース](../assets/my-automation-hub-resources.png)

> 完了までに数分の時間がかかる場合があります。

お疲れさまでした。Automation Hub が正常にインストールされている。

> **_警告：_** 次のチャレンジにアクセスする前に、プライベート Automation Hub をデプロイした Pod が稼働している必要があります。次のチャレンジにアクセスしようとすると、Pod が起動する前にアクセスできなくなります。Red Hat OpenShift ダッシュボードで `Pod` のステータスを表示し、`Workloads` ドロップダウンメニューで Pods を選択します。実行中のすべての Pod のビューが表示されます。これらの Pod は、Ansible Automation Platform のインストールプロセスの一部です。

![AHub Pod](../assets/ahub-pods.png)

ターミナルでこれを表示するには、ターミナル 1 タブを選択し、以下のコマンドを実行します。

```
watch -n 1 oc get pods -n ansible-automation-platform
```

> **_注記：_** CrashLoopBackOff は、プライベート Automation Hub のインストールが完了している間に特定の Pod で可能なステータスです。

Pod を監視する以外に、デプロイメントが以下を使用して完全にロールアウトされているかどうかを確認することもできます。

```
oc rollout status deployment my-automation-hub-web -n ansible-automation-platform
```

次のチャレンジでは、自動化コントローラーと Automation Hub ダッシュボードにアクセスします。
