---
slug: ahub-install
id: dvtciaf9iguk
type: challenge
title: Operator 経由でのプライベート Automation Hub のインストール
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
制限時間: 600
---
前の課題では、AAP から自動コントローラーコンポーネントをインストールしました。インストールが完了したので、続いて AAP Operator の詳細ウィンドウからプライベート Automation Hub コンポーネントをインストールします。

## Automation Hub のインストール

* `Operators-> Installed Operators-> Ansible Automation Platform` Operator の詳細ウィンドウで、`Automation Hub` というラベルの付いたタブを選択します。

![Operator Details](../assets/ahub_tab.png)

* 選択したら、`Create AutomationHub` というラベルの付いた青いボタンを選択します。
* `Create AutomationHub` ウィンドウで、プライベート Automation Hub の名前を指定します (例: `my-automation-hub`)。`Storage Type` ドロップダウンで `File` を選択します。

> **_注記:_**`Storage Type` には、`S3` や `Azure` などの他のオプションも利用できます。

* Form ビューの下部にある青い `Create` ボタンをクリックします。

![AHub Form View](../assets/ahub_form.png)

> **_注記:_** このデモのラボでは、プライベート Automation Hub のインストールにデフォルトを使用します。Form ビューを介してプライベート Automation Hub を設定する以外に、YAML ビューを介してカスタマイズしたり、Form ビュー内の `Advanced configuration` タブを介して詳細設定をセットアップしたりできます。

* 作成が行われることで、多くの OpenShift リソースが `my-automation-hub` の新しいインストール用に作成されます。

![AHub Resources](../assets/my-automation-hub-resources.png)

> **_注記:_** 完了までに数分の時間がかかる場合があります。

お疲れさまでした。Automation Hub が正常にインストールされました。

> **_警告:_** 次の課題にアクセスする前に、プライベート Automation Hub をデプロイした Pod が稼働している必要があります。Pod が起動する前に次の課題にアクセスしようとすると、アクセスできなくなります。Red Hat OpenShift ダッシュボードで Pod のステータスを表示できます。`Workloads` ドロップダウンで `Pod` を選択してください。実行中のすべての Pod のビューが表示されます。これらの Pod は、Ansible Automation Platform のインストールプロセスの一部になります。

![AHub Pods](../assets/ahub-pods.png)

これをターミナル上で表示したい場合は、ターミナル 1 タブを選択し、以下のコマンドを実行してください。

```
watch -n 1 oc get pods -n ansible-automation-platform
```

> **_注記:_** プライベート Automation Hub のインストールが完了するまでの間、一部の Pod のステータスが CrashLoopBackOff になる可能性があります。

Pod の表示とは別に、デプロイメントが完全にロールアウトされたかどうかを、以下の方法で確認することもできます。

```
oc rollout status deployment my-automation-hub-web -n ansible-automation-platform
```

次の課題では、自動コントローラーと Automation Hub ダッシュボードにアクセスします。
