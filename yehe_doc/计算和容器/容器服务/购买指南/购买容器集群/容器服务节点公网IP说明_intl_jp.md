パブリックネットワークから直接業務セキュリティにアクセスできないが、パブリックネットワークへのアクセスができるようにするという要望がある場合、Tencent Cloudの[NATゲートウェイ](https://intl.cloud.tencent.com/document/product/215/4975)をご利用ください。以下でNATゲートウェイを使用してパブリックネットワークにアクセスする方法をご紹介します。

## パブリックネットワークIP
デフォルトでは、クラスターを作成する時、クラスターのノードにパブリックネットワークIP
を割り当てます。割り当てられたパブリックネットワークIPは以下の役割を果たします：
- パブリックネットワークIPでクラスターのノードマシンにログインします。
- パブリックネットワークIPでパブリックネットワークサービスにアクセスします。

## パブリックネットワーク帯域幅
パブリックネットワークサービスを作成する時、パブリックネットワークロードバランサーが使用するのはノードの帯域幅とトラフィックです。パブリックネットワークサービスを提供する場合、ノードにパブリックネットワーク帯域幅があることを確保する必要があります。業務がパブリックネットワークを必要としなければ、パブリックネットワーク帯域幅を購入しなくても構いません。

## NATゲートウェイ
CVMはElastic IPアドレスをバインドしません。InternetにアクセスするすべてのトラフィックはNATゲートウェイ経由で転送されます。このソリューションでは、CVMがInternetにアクセスするトラフィックは、内部ネットワーク経由でNATゲートウェイに転送されるため、CVM購入時のパブリックネットワークの帯域幅に制限されません。また、NATゲートウェイが生じたネットワークトラフィックはCVMのパブリックネットワークのアウトバンドを占有しません。NATゲートウェイ経由でInternetにアクセスするには、以下を実施してください：

### ステップ1：NATゲートウェイを作成します
1. [VPCコンソール](https://console.cloud.tencent.com/vpc/vpc?rid=1)にログインし、左側のナビゲーションバーで【[NATゲートウェイ](https://console.cloud.tencent.com/vpc/nat?rid=1)】をクリックします。
2. 「NATゲートウェイ」管理画面で、**新規作成**をクリックします。
3. 表示された「NATゲートウェイの新規作成」ウィンドウに、以下のパラメータを記入します。
 - ゲートウェイ名：カスタム。
 - 所属ネットワーク：NATゲートウェイサービスのプライベートネットワークを選択します。
 - ゲートウェイタイプ：必要に応じて選択してください。ゲートウェイタイプは作成後にも変更可能です。
 - アウトバンド帯域幅上限：必要に応じて選択します。
 - Elastic IP：NATゲートウェイにElastic IPを割り当てます。既存Elastic IPを選択するか新規購入してElastic IPを割り当ててください。
4. **作成**をクリックして、NATゲートウェイの作成を完了します。
>! NATゲートウェイ作成時にリース料金は1時間凍結されます。

### ステップ2：関連サブネットワークが関連付けられたルーティングテーブルを設定します

>? NATゲートウェイを作成した後、サブネットのトラフィックをNATゲートウェイに転送するように、VPCコンソールのルーティングテーブル画面でルーティングルールを設定する必要があります。
>

1. 左側のナビゲーションバーで【[ルーティングテーブル](https://console.cloud.tencent.com/vpc/route?rid=1)】をクリックします。
2. ルーティングテーブル一覧で、Internetにアクセスするサブネットワークが関連付けられたルーティングテーブルのID/名前をクリックして、ルーティングテーブルの詳細画面に入ります。
3. 「ルーティングポリシー」欄で、「ルーティングポリシー追加」をクリックします。
4. 表示された「新規ルーター」ウィンドウに、**デスティネーション**を記入し、**次のホップのタイプ**に**NATゲートウェイ**、**次のホップ**に作成したNATゲートウェイのIDを指定します。
5. **OK**をクリックします。
上記のように設定した後、このルーティングテーブルに関連付けられたサブネットワークにおけるCVMがIntenetにアクセスするトラフィックはNATゲートウェイに転送されます。

## その他のソリューション

### 案1：Elastic IPアドレスを使用します
CVMはElastic IPアドレスだけをバインドし、NATゲートウェイを使用しません。この案では、CVMがInternetにアクセスするすべてのトラフィックは、Elastic IPアドレス経由で転送され、CVM購入時のパブリックネットワークの帯域幅に制限されます。パブリックネットワークへのアクセスによって生じた料金は、CVMネットワーク課金モデルによって計算されます。
使用方法：[Elastic IPアドレス使用手引書](https://intl.cloud.tencent.com/document/product/215/4958#.E6.93.8D.E4.BD.9C.E6.8C.87.E5.8D.97)をご参照ください。

### 案2：NATゲートウェイとastic IPアドレス両方を使用します
NATゲートウェイとastic IPアドレス両方を使用する案では、CVMからInternetへのアクセスによって生じたすべてのトラフィックは、内部ネットワーク経由でNATゲートウェイに転送されます。返されたパケットもNATゲートウェイ経由でCVMに転送されます。この部分のトラフィックは、CVM購入時のパブリックネットワークの帯域幅に制限されません。NATゲートウェイが生じたネットワークトラフィックはCVMのパブリックネットワークのアウトバンドを占有しません。InternetからのトラフィックがCVMのElastic IPアドレスにアクセスする場合、CVMが返したパケットは全部Elastic IPアドレス経由で転送され、生じたパブリックネットワークのアウトバンドトラフィックは、CVM購入時のパブリックネットワークの帯域幅に制限されます。パブリックネットワークへのアクセスによって生じた料金は、CVMネットワーク課金モデルによって計算されます。

>! ご利用中のアカウントで帯域幅パックによる帯域共有機能をアクティブ化した場合、NATゲートウェイが生じたアウトバンドトラフィックは帯域幅パック全体に基づき計算されます(0.12ドル/GBのネットワークトラフィック料金を重複して請求しません）。NATゲートウェイの高いアウトバンドによって多額な帯域幅パック料金が生じることを防ぐために、NATゲートウェイのアウトバンドに制限をかけることを推奨します。
