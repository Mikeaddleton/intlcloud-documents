
## TKE課金説明
現時点では、TKEのご利用自体は無料ですが、実際に使用されたクラウドリソースに応じて料金を請求します。TKE利用時に以下の製品が使用される場合があります。詳しくは、具体的な製品の課金説明をご参照ください。

- [CVM課金モデル](https://intl.cloud.tencent.com/document/product/213/2180)
- [CBS価格一覧](https://intl.cloud.tencent.com/document/product/213/2255)
- [ロードバランサー課金説明](https://intl.cloud.tencent.com/document/product/214/8848)

>! TKEはKubernetesベースの宣言式サービスです。TKEが作成したロードバランサーCLBやクラウドディスクCBSなどのIaaSサービスリソースを必要としなくなる場合、具体的なサービスリソース画面から削除するのではなく、TKEコンソールから該当するサービスリソースを削除してください。そうしない場合、TKEは削除されたサービスリソースを再作成し、関連の料金が請求されます。例えば、TKEにロードバランサーCLBサービスリソースがすでに作成されているとします。ロードバランサーコンソールからこのCLBインスタンスを削除すると、TKEは宣言式APIにより新しいCLBインスタンスを作成します。

## EKS課金説明
EKSは、後払いの従量制課金モデルを採用し、実際に構成したリソースと使用時間に応じて料金を請求するため、事前に支払う必要がありません。詳しくは、[イラスチッククラスター課金概要](https://intl.cloud.tencent.com/document/product/457/34054)をご参照ください。

