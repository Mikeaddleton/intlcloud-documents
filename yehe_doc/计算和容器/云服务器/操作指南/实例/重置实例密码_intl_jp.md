## 概要
パスワードを忘れた場合は、コンソールでインスタンスのログインパスワードをリセットできます。このドキュメントでは、Cloud Virtual Machine（CVM）管理コンソールでインスタンスのログインパスワードを変更する方法について説明します。

<dx-alert infotype="notice" title="">

- 「シャットダウン」状態のインスタンスは、パスワードのリセット操作を直接実行できます。
- 「実行中」状態のインスタンスの場合は、コンソールを介してインスタンスのパスワードをリセットする過程でインスタンスが閉じられます。データの損失を防ぐため、あらかじめ操作時間の計画を立てておいてください。業務が少ないときに操作して、影響を最小限に抑えることをお勧めします。
</dx-alert>


## 操作手順
<dx-tabs>
::: 単一インスタンスのパスワードをリセットする
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
   - **リストビュー**：下図のように、パスワードをリセットしたいCVMが存在する行の右側の**その他** > **パスワード/キー** > **パスワードリセット**を選択します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/9317997308e40e06dcacc64cac24dd41.png)
   - **タブビュー**：下図のように、パスワードをリセットしたいCVMページで、**パスワードリセット**をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/032ecb8f3544bb17892decba6c955d8a.png)
3. 下図のように、「パスワードの設定」手順で、「ユーザー名」のタイプを選択し、パスワードをリセットしたいユーザー名と、対応する「新しいパスワード」と「パスワードの確認」を入力して**次へ**をクリックします。
<dx-alert infotype="notice" title="">
そのうち「ユーザー名」タイプのデフォルトは「システムデフォルト」であり、対応するOSのデフォルトユーザー名（Windowsシステムのデフォルトユーザー名は`Administrator`、Ubuntuシステムのデフォルトユーザー名は`ubuntu`、その他のバージョンのLinuxシステムのデフォルトは`root`）が使用されます。別のユーザー名を指定する必要がある場合は、「ユーザー名の指定」を選択し、対応するユーザー名を入力してください。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/420c83619601563c1c3c0c64c0bf533d.png"/>
4. 「プロンプトの停止」の手順では、インスタンスのステータスに応じて、パスワードのリセット操作が次のように異なります。
 - 下図のように、パスワードをリセットしたいインスタンスが「**実行中**」状態の場合は、「強制シャットダウンに同意する」にチェックを入れ、**パスワードリセット**をクリックしてリセットを完了してください。
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - 下図のように、パスワードをリセットしたいインスタンスが「**シャットダウン**」状態の場合は、**パスワードリセット**をクリックしてリセットを完了してください。
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)   

:::
::: 複数インスタンスのパスワードをリセットする

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 下図のように、インスタンスの管理ページで、パスワードのリセットが必要なCVMを選択し、上の**パスワードリセット**をクリックします。
![](https://main.qcloudimg.com/raw/38b9be9d0b1b6890f9b07852e91c8bd3.png)
3. 下図のように、「パスワード設定」手順で、「ユーザー名」のタイプを選択し、パスワードをリセットしたいユーザー名と、対応する「新しいパスワード」と「パスワードの確認」を入力して**次へ**をクリックします。
<dx-alert infotype="notice" title="">
そのうち「ユーザー名」タイプのデフォルトは「システムデフォルト」であり、対応するOSのデフォルトユーザー名（Windowsシステムのデフォルトユーザー名は`Administrator`、Ubuntuシステムのデフォルトユーザー名は`ubuntu`、その他のバージョンのLinuxシステムのデフォルトは`root`）が使用されます。別のユーザー名を指定する必要がある場合は、「ユーザー名の指定」を選択し、対応するユーザー名を入力してください。
</dx-alert>
![](https://main.qcloudimg.com/raw/1abf9af8eb892191acc3998bb5845dea.png)
4. 「プロンプトの停止」の手順では、インスタンスのステータスに応じて、パスワードのリセット操作が次のように異なります。
 - 下図のように、パスワードをリセットしたいインスタンスが「**実行中**」状態の場合は、「強制シャットダウンに同意する」にチェックを入れ、**パスワードリセット**をクリックしてリセットを完了してください。
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - 下図のように、パスワードをリセットしたいインスタンスが「**シャットダウン**」状態の場合は、**パスワードリセット**をクリックしてリセットを完了してください。
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)    

:::
</dx-tabs>

## 関連する質問
Windowsインスタンスのパスワードのリセットに失敗した場合は、[Windowsインスタンス：パスワードリセットの無効](https://intl.cloud.tencent.com/document/product/213/35720)を参照してトラブルシューティングを行い、問題を解決することができます。
