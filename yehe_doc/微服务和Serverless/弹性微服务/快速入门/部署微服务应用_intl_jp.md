## 概要

ここでは、Spring Cloudで開発されたプロデューサーとコンシューマーのDemoアプリケーションプログラムにより、JARパッケージのアップロードデプロイ方法を採用して、マイクロサービスアプリケーションをTEMにデプロイし、アプリケーションを相互に呼び出して、パブリックネットワークでアクセスできるようにする方法をご説明します。


##  前提条件

アプリケーションのデプロイを開始する前に、[準備作業](https://intl.cloud.tencent.com/zh/document/product/1094/41383)を読んで完了していることを確認してください。


## 操作手順

### 手順1：Demoアプリケーションの取得

異なるレジストリを使用するSpring Cloudマイクロサービスアプリケーションのデモンストレーションを行うため、Eurekaレジストリを使用する、2グループのプロデューサーとコンシューマーのDemoアプリケーションをご用意しています。

これらのDemoアプリケーションの[ソースコード](https://github.com/tencentyun/tem-demo)をGithubで表示するか、またはJARパッケージによって直接ダウンロードすることができます。

 Eurekaレジストリ：[Provider Demo](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/eureka-provider-0.0.1-SNAPSHOT.jar)と[Consumer Demo](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/eureka-consumer-0.0.1-SNAPSHOT.jar)。




### 手順2：レジストリの設定

Spring Cloud Demoアプリケーションのデプロイを開始する前に、**環境**に**レジストリ**リソースを設定する必要があります。[環境リソースの追加](https://intl.cloud.tencent.com/zh/document/product/1094/40361)の操作手順を参照して、選択したアプリケーションに対応するレジストリを追加してください。

### ステップ3：アプリケーションのデプロイ

1. TEMコンソールの[**アプリケーション管理**](https://console.cloud.tencent.com/tem/application)ページの上部で、アプリケーションのデプロイリージョンを選択します。
2. **新規作成**をクリックして、アプリケーションの新規作成ページに進み、アプリケーション情報を入力します。   
   ![](https://qcloudimg.tencent-cloud.cn/raw/f83989eff2132de907cc5da3c74e380a.png)
3. **サブミット**をクリックし、ポップアップボックスの**OK**をクリックして、アプリケーションのデプロイに移動します。
4. アプリケーションデプロイページで、アプリケーションの具体的な状況に応じて関連パラメータを設定します。
   ![](https://main.qcloudimg.com/raw/5cde618b2418fca282ad75ac56f8dcd0.png)
   - パッケージのアップロード：パッケージをアップロードします。
   - 環境の公開：今作成した環境を選択します。
   - Spring Cloudアプリケーションに対して、選択した**パブリッシュ環境**が**レジストリ**にバインドされている場合、デプロイ時に**レジストリ情報の自動挿入**を選択することができます。登録と検出の具体的な操作フローと設定情報については、[アプリケーションの登録と検出](https://intl.cloud.tencent.com/zh/document/product/1094/40960)をご参照ください。
   - アプリケーションでその他の詳細オプションを設定する必要がある場合は、[アプリケーションの作成とデプロイ](https://intl.cloud.tencent.com/zh/document/product/1094/40362)をご参照ください。
5. **デプロイ**をクリックして、providerアプリケーションのデプロイを完了します。
6. **手順1～5**を繰り返して、consumerアプリケーションのデプロイを完了します。



### 手順4：登録済みアプリケーションの確認

1. デプロイするアプリケーションインスタンスの実行が開始されたら、マイクロサービスエンジンコンソールの[レジストリ](https://console.cloud.tencent.com/tse/zookeeper)に進み、リストからデプロイ環境にバインドされているレジストリを選択します。
2. レジストリの詳細ページで、**サービス管理**ページを選択し、providerとconsumerのアプリケーションの登録が成功しているか確認します。
   



### 手順5：アクセスの検証

デプロイおよび登録に成功したプロバイダ-コンシューマーアプリケーションは、コンシューマーアプリケーションの**環境**にアクセス設定を作成することにより、パブリックネットワークを介してアクセスすることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/ce11ddfb61158ec7874a6a2ef643144a.png)

1. TEMコンソールの[**環境**](https://console.cloud.tencent.com/tem/env)ページの上部で、アプリケーションをデプロイするリージョンを選択します。
2. アプリケーションがデプロイされている環境カード上の**詳細の表示**をクリックして詳細ページに進み、上部にある**アクセス管理**を選択します。
3. **新規作成**をクリックしてアクセス設定の新規作成ページに進み、アクセス設定情報を入力します。
   ![](https://main.qcloudimg.com/raw/7a960a81645810e39cefe7c969b08996.png)
   
   - ネットワークタイプ：パブリックネットワークアクセスです。環境内へのアクセスが必要な場合は、[アプリケーションの作成とデプロイ](https://intl.cloud.tencent.com/zh/document/product/1094/40362)をご参照ください。
   - Cloud Load Balance：自動作成
   - プロトコルとポート：HTTP:80とHTTPS:443をサポートし、かつHTTPSドメイン名バインド証明書をサポートします。DemoアプリケーションにはHTTP：80を選択してください。
   - 転送構成：
     - ドメイン名：既存ドメイン名のバインドをサポートしています。ドメイン名がない場合は、デフォルトでIPv4 IPが割り当てられます。Demoアプリケーションにはデフォルトで割り当てられたIPを使用してください。
     - パス：デフォルトは「/」で、実際の状況に応じて設定します
     バックエンドアプリケーション：デプロイしたconsumer Demoアプリケーションを選択します。
     - アプリケーションポート：eureka-consumerアプリケーションはポート8003を使用してください。
   - サーバー証明書：HTTPプロトコルを選択する場合は、サーバー証明書を選択する必要があります。既存の証明書が適切でない場合は、[サーバー証明書の新規作成](https://console.cloud.tencent.com/clb/cert)に移動できます
4. **確定**をクリックして、アクセス設定の新規作成を完了します。アプリケーションのパブリックネットワークアクセスIPは、環境詳細ページの**アクセス管理**で確認できます。
   ![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)
5. ブラウザに次のURLを入力します。
	```plaintext
	http://パブリックネットワークアクセスIP/ping-provider
	```
	次の結果が返された場合、アプリケーションのデプロイは成功していることを意味します。
	```plaintext
	pong from eureka-provider 
	```
