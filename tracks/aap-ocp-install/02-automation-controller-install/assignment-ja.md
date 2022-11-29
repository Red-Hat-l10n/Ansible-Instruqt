---
slug: automation-controller-install
id: rtiw0rhtalbx
type: challenge
title: Operator を介した自動コントローラーのインストール
タブ:
- title: Web コンソール
  type: website
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: ターミナル 1
  type: terminal
  hostname: crc
難易度: 基本
制限時間: 600
---
前の課題では、Ansible Automation Platform (AAP) Operator をインストールしました。インストールが完了したので、続いて AAP Operator の詳細ウィンドウから、自動コントローラーコンポーネントをインストールします。

## 自動コントローラーのインストール

* Operator の詳細ウィンドウで、`Automation Controller` というラベルの付いたタブを選択します。

![Operator Details](../assets/automation_controller_tab.png)

* 選択したら、`Create AutomationController` というラベルの付いた青いボタンを選択します。
* `Create AutomationController` ウィンドウで、自動コントローラーの名前を指定します (例: `my-automation-controller`)。
* Form ビューの下部にある青い `Create` ボタンをクリックします。

![AAP Form View](../assets/operator_form_1.png)

> **_注記:_** このデモのラボでは、自動コントローラーのインストールにデフォルトを使用します。Form ビューを介して自動コントローラーを設定する以外に、YAML ビューを介してカスタマイズしたり、Form ビュー内の `Advanced configuration` タブを介して詳細設定をセットアップしたりできます。

* 作成が行われることで、多くの OpenShift リソースが `my-automation-controller` の新しいインストール用に作成されます。

![AAP Resources](../assets/my-automation-controller-resources.png)

> **_注記:_** 完了までに数分の時間がかかる場合があります。

お疲れさまでした。自動コントローラーが正常にインストールされました。

> **_警告:_** 次の課題にアクセスする前に、自動コントローラーをデプロイした Pod が稼働している必要があります。Pod が起動する前に次の課題にアクセスしようとすると、アクセスできなくなります。Red Hat OpenShift ダッシュボードで Pod のステータスを表示できます。`Workloads` ドロップダウンで `Pod` を選択してください。実行中のすべての Pod のビューが表示されます。`my-automation-controller-<id>-<id>` が Pod の作成を終了することを明示的に確認しています。これらの Pod は、Ansible Automation Platform のインストールプロセスの一部になります。

![AAP Pods](../assets/controller-pods.png)

これをターミナル上で表示したい場合は、`Terminal 1` タブを選択し、以下のコマンドを実行してください。

```
watch -n 1 oc get pods -n ansible-automation-platform
```

注記: 自動コントローラーのインストールが完了するまでの間、一部の Pod のステータスが CrashLoopBackOff になる可能性があります。

Pod の表示とは別に、デプロイメントが完全にロールアウトされたかどうかを、以下の方法で確認することもできます。

```
oc rollout status deployment my-automation-controller -n ansible-automation-platform
```


次の課題では、自動コントローラーのダッシュボードにアクセスします。
