---
slug: automation-controller-install
id: rtiw0rhtalbx
type: challenge
title: Operator を使用した自動コントローラーのインストール
タブ:
- Web コンソール
  type: website
  url: https://console-openshift-console.crc-gh9wd-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: ターミナル 1
  type: terminal
  hostname: crc
難易度: 基本
timelimit: 600
---
以前のチャレンジでは、Ansible Automation Platform (AAP) Operator をインストールしました。インストールが完了すると、AAP Operator の詳細ウィンドウ内から Automation Controller コンポーネントをインストールし続けます。

## 自動化コントローラーのアップグレード

* Operator details ウィンドウで、`Automation Controller` のラベルが付いたタブを選択します。

![Operator の詳細](../assets/automation_controller_tab.png)

* 選択したら、`Create AutomationController` というラベルの青いボタンを選択します。
* `Create AutomationController` ウィンドウで、自動化コントローラーの名前を指定します（例： `my-automation-controller`）。
* Form ビューの下部で、青色の `Create` ボタンをクリックします。

![AAP フォームビュー](../assets/operator_form_1.png)

> **_注記：_** このデモラボでは、自動化コントローラーのインストールにデフォルトを使用します。Form ビューで自動化コントローラーを設定する以外に、YAML ビューを使用してカスタマイズしたり、Form ビューの `Advanced configuration` タブから詳細設定を設定したりできます。

* 作成が行われると、`my-automation-controller` の新規インストール用に、OpenShift リソースの多くは作成されます。

![AAP リソース](../assets/my-automation-controller-resources.png)

> 完了までに数分の時間がかかる場合があります。

お疲れさまでした。自動化コントローラーが正常にインストールされました。

> **_警告：_** 次のチャレンジにアクセスする前に、自動化コントローラーをデプロイした Pod が稼働している必要があります。次のチャレンジにアクセスしようとすると、Pod が起動する前にアクセスできなくなります。Red Hat OpenShift ダッシュボードで `Pod` のステータスを表示し、`Workloads` ドロップダウンメニューで Pods を選択します。実行中のすべての Pod のビューが表示されます。明示的に、`my-automation-controller-<id>-<id>` Pod の作成が完了したことを確認します。これらの Pod は、Ansible Automation Platform のインストールプロセスの一部です。

![AAP Pod](../assets/controller-pods.png)

ターミナルでこれを表示するには、ターミナル `1 タブを選択し`、以下のコマンドを実行します。

```
watch -n 1 oc get pods -n ansible-automation-platform
```

注記：自動化コントローラーのインストールが完了している間に、特定の Pod で CrashLoopBackOff のステータスを使用できます。

Pod を監視する以外に、デプロイメントが以下を使用して完全にロールアウトされているかどうかを確認することもできます。

```
oc rollout status deployment my-automation-controller -n ansible-automation-platform
```


次のチャレンジでは、自動化コントローラーダッシュボードにアクセスします。
