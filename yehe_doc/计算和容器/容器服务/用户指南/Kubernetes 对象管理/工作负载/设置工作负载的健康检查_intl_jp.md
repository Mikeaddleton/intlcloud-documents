Tencent CloudコンテナのカーネルはKubernetesに基づいています。Kubernetesは、コンテナを定期的にプローブし、プローブ結果に基づいてコンテナのヘルス状態を判断し、追加のアクションを実行することをサポートします。

## 健康診断のタイプ

健康診断は次のカテゴリに分類されます：
- **コンテナアクティブ診断**：コンテナがアクティブであるかどうかを検出するために使用されます。psコマンドを実行してプロセスが存在するかどうかを確認するとに類似しています。コンテナアクティブ診断が失敗した場合、クラスターはコンテナをリスタートします。コンテナアクティブ診断が成功した場合、いかなるアクションを実行しません。
-**コンテナ準備診断**：コンテナがユーザーのリクエストの処理を開始する準備ができているかどうかを検出するために使用されます。例えば、プログラムの起動に時間がかかる場合、サービスを提供する前に、ディスクデータをロードするか、外部モジュールに依存して起動を完了してください。この場合、コンテナ準備診断を使用してプログラムのプロセスを確認し、プログラムの起動が完了したかどうかを確認できます。コンテナ準備診断が失敗した場合、クラスターはコンテナへのアクセスリクエストをブロックします。コンテナ準備診断が成功した場合、コンテナへのアクセスが開放されます。

## 健康診断方法

<span id="TCPPortProbe"></span>
### TCPポートプローブ

### TCPポートプローブの原理は次のとおりです：
TCP通信サービスを提供するコンテナの場合、クラスターはコンテナへのTCP接続を定期的に確立します。接続が成功した場合、プローブは成功します。それ以外の場合、プローブは失敗します。TCPポートプローブ方法を選択すると、コンテナがリッスンするポートを指定してください。
例えば、redisコンテナの場合、そのサービスポートは6379です。コンテナでTCPポートプローブを構成し、プローブポートを6379として指定する場合、クラスターはコンテナのポート6379でTCP接続を定期的に開始します。接続が成功した場合、診断は成功します。それ以外の場合、診断は失敗します。

<span id="HTTPRequestProbe"></span>
### HTTPリクエストプローブ

HTTPリクエストプローブは、HTTP/HTTPSサービスを提供するコンテナ用であり、クラスターはコンテナにHTTP/HTTPS GETリクエストを定期的に送信します。HTTP/HTTPS responseのリターンコードが200〜399の範囲にある場合、プローブは成功します。それ以外の場合、プローブは失敗します。HTTPリクエストプローブを使用するには、コンテナがリッスンするポートとHTTP/HTTPSリクエストパスを指定する必要があります。
例えば、HTTPサービスを提供するコンテナの場合、サービスポートが80で、HTTPチェックパスが`/health-check`の場合、クラスターはコンテナに`GET http://containerIP:80/health-check`リクエストを定期的に送信します。

### 実行コマンドのチェック

実行コマンドのチェックは、ユーザーがコンテナ内の実行可能コマンドを指定する必要がある強力なチェック方法です。クラスターはコンテナ内でコマンドを定期的に実行します。コマンドの返された結果が0の場合、チェックは成功します。それ以外の場合、チェックは失敗します。
[TCPポートプローブ](#TCPPortProbe)および[HTTPリクエストプローブ](#HTTPRequestProbe)の両方とも、実行コマンドをチェックすることで置き換えることができます：
- TCPポートプローブの場合、コンテナのポートにconnectするプログラムを作成できます。connectが成功した場合、スクリプトは0が返されます。それ以外の場合、-1が返されます。
- HTTPリクエストプローブでは、コンテナをwgetしてresponseのリターンコードをチェックするスクリプトを生成できます。例えば、`wget http://127.0.0.1:80/health-check`。リターンコードが200～399の範囲にある場合、スクリプトは0が返されます。それ以外の場合、-1が返されます。

#### 注意事項
- 実行する必要のあるプログラムは、コンテナのイメージに配置する必要があります。そうしないと、プログラムが見つからないため、実行が失敗します。
- 実行されるコマンドがshellスクリプトの場合、実行コマンドとしてスクリプトを直接指定できません。スクリプトのインタプリタを追加する必要があります。例えば、スクリプトが`/data/scripts/health_check.sh`の場合、実行コマンドを使用してチェックするとき、指定するプログラムは次のようになります：
```
sh 
/data/scripts/health_check.sh 
```
設定手順では、例として[Tencent Kubernetes Engineコンソール](https://console.cloud.tencent.com/tke2)を使用してDeploymentを作成します：
 1. クラスター「Deployment」ページでは、**新規作成**をクリックします。
 2. 「Workloadの新規作成」ページへ進み、「コンテナ内のインスタンス」モジュール下方の**詳細設定を表示する**を選択します。
  3. 「コンテナの健康診断」では、例として**アクティブ診断**を選択し、次のパラメータを設定します。
   - **チェック方法**：「実行コマンドのチェック」を選択します。
   - **実行コマンド**：次のように入力します。
   ```
sh 
/data/scripts/health_check.sh 
   ```
 4. その他のパラメータ設定については、[Deployment管理](https://intl.cloud.tencent.com/document/product/457/30662)をご参照ください。

## その他の共通パラメータ

- **起動レイテンシー**：単位は秒。コンテナを起動してからプローブを開始する時間を指定します。例えば、起動レイテンシーが5に設定されている場合、健康診断はコンテナの起動から5秒後に開始されます。
- **間隔時間**：単位は秒。健康診断の頻度を指定します。例えば、間隔が10に設定されている場合、クラスターは10秒ごとにチェックします。
- **レスポンスタイムアウト**：単位は秒。健康プローブのタイムアウト時間を指定します。TCPポートプローブ、HTTPリクエストプローブ、実行コマンドチェックの3つの方法に対応して、それぞれTCP接続のタイムアウト時間、HTTPリクエストレスポンスのタイムアウト時間、実行コマンドのタイムアウト時間を示します。
- **健康閾値**：単位は回。コンテナが正常であると判断する前に、健康診断が連続して成功する回数を指定します。例えば、健康閾値が3に設定されている場合、プローブが3回連続して成功した場合にのみ、コンテナが正常であると見なされることを意味します。
>! 健康診断のタイプがアクティブ診断の場合、健康閾値は1のみであり、ユーザーが設定した他の値は無効と見なされます。
- **不健康閾値**：単位は回。コンテナが不健康であると判断する前に、健康診断が連続して失敗する回数を指定します。例えば、不健康閾値が3に設定されている場合、プローブが3回連続して失敗した場合にのみ、コンテナが不健康であると見なされることを意味します。
