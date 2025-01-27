## 製品紹介
テンセントクバネティスエンジン（Tencent Kubernetes Engine、TKE）は、高い拡張性と性能を有するコンテナ管理サービスです。ホストされているCVMインスタンスクラスターで、アプリケーションを手軽に実行することができます。このサービスを使用すると、クラスター管理インフラストラクチャをインストール・運用・保守・拡張する必要がありません。簡単なAPI呼び出しだけで、Dockerアプリケーションの開始と停止、クラスターの完全な状態の照会を行い、さまざまなクラウドサービスを使用することができます。お客様はリソース要件および可用性要件に基づいてクラスター内のコンテナの配置を調整し、業務やアプリケーションの特定の要件を満たすことができます。

テンセントクバネティスエンジンはネイティブのKubernetesに基づき、コンテナを中心としたソリューションを提供し、ユーザーの開発、テスト、運営維持過程の環境問題を解決し、ユーザーのコスト削減と効率向上を支援します。Tencent CloudコンテナサービスはネイティブのKubernetes APIと完全に互換性があり、Tencent CloudのCloud Block StorageやCloud Load BalancerなどのKubernetesプラグインを拡張すると同時に、Tencent Cloudのプライベートネットワークを基礎とし、高信頼性、高性能のネットワークプランを実現しました。

## 用語の説明
テンセントクバネティスエンジンを利用するには、次のような基本的な概念が含まれます。
- **クラスター**：コンテナの実行に必要なクラウドリソースの集まりで、複数のCVMやロードバランサなどのクラウドリソースが含まれています。
- **インスタンス（Pod）**：1つまたは複数の関連付けられたコンテナで構成されたインスタンスです。これらのコンテナは同一のストレージとネットワークスペースを共有します。
- **ワークロード**：Podコピーの作成、スケジューリングおよびライフサイクル全体の自動制御を管理するためのKubernetesリソースオブジェクト。
- **Service**：同じ構成の複数のインスタンス（Pod）と、これらのインスタンス（Pod）にアクセスするルールから構成されるマイクロサービス。
- **Ingress**：外部HTTP（S）トラフィックをサービス（Service）にルーティングするために使用される一連の規則です。
- **アプリケーション**：TKEが統合したHelm 3.0関連機能のことで、helm chart、コンテナイメージ、ソフトウェアサービスなどのさまざまな製品やサービスを作成することができます。
- **イメージリポジトリ**：コンテナサービスのデプロイに使用されるDockerイメージを保持します。


## 使用手順
コンテナサービスの使用プロセスを次の図に示します：
![](https://main.qcloudimg.com/raw/4a7b3a025c99e264eda78431ee964552.png)

1.　ロール権限授与
   TKEコンソールに登録してログインし、サービス認証を完了してリソースのアクション権限を取得すると、コンテナサービス製品を使用できます。
2.　クラスターの作成
   新規クラスターをカスタマイズすることも、テンプレートを使用して新規クラスターを作成することもできます。
3.　ワークロードのデプロイ
   ワークロードのデプロイには、イメージデプロイ、YAMLファイルオーケストレーションの両方の方法を使用できます。詳細については、[ワークロード管理](https://intl.cloud.tencent.com/document/product/457/30662)をご参照ください。
4.ワークロードの作成後、Podライフサイクルは監視、アップグレード、スケーリングなどによって管理されます。



## 製品料金
コンテナサービスにはサービス自体の料金は当分かかりませんが、ユーザーは実際に使用したクラウドリソースに応じて料金を支払うだけです。料金体系と具体的な料金については、[課金の説明](https://intl.cloud.tencent.com/document/product/457/6770)をご参照ください。

## 関連サービス

- 複数のCVMを購入してコンテナサービスクラスターを構成し、コンテナをCVM内で稼働させます。詳細については、[CVM製品ドキュメント](https://intl.cloud.tencent.com/document/product/213)をご参照ください。
- クラスターをプライベートネットワークの下に構築し、クラスター内のCVMを異なるアベイラビリティーゾーンのサブネットに割り当てることができます。詳細については、[プライベートネットワーク製品ドキュメント](https://intl.cloud.tencent.com/document/product/215)をご参照ください。
- CLBを使用すると、複数のCVMインスタンスにまたがるクライアントリクエストトラフィックを自動的に割り当て、CVM内のコンテナに転送できます。詳細については、[CLB製品ドキュメント](https://intl.cloud.tencent.com/zh/document/product/214)をご参照ください。
- Cloud Monitorサービスを使用して、TKEクラスターとコンテナインスタンスの実行統計データを監視できます。詳細については、[Cloud Monitor製品ドキュメント](https://intl.cloud.tencent.com/document/product/248)をご参照ください。




