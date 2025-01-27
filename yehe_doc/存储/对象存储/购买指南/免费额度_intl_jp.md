## 概要
COSは全新規ユーザー（COSサービスを初めてアクティブ化したユーザー）向けに一定量の無料利用枠を提供しています。**標準ストレージタイプ**のデータによって発生する標準ストレージ容量料金に充当できます。無料利用枠の明細は下表をご参照ください。 

| 対象者 | 無料利用枠          | 有効期間 |
| -------- | ----------------- | ------ |
| 新規ユーザー | 50GB標準ストレージ容量 | 6か月  |

>?ストレージ量は2進数で計算されます。例えば、1TB = 1024GBとなります。

## 無料範囲

リージョンの範囲に基づき、無料利用枠は**パブリッククラウドリージョン**に適用されます。リージョンの区分については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)でお調べください。

[課金項目](https://intl.cloud.tencent.com/document/product/436/33776)の範囲に基づいてCOSが提供する無料**標準ストレージ容量**の対象範囲については、次の表をご参照ください。

> !
>
>- ユーザーの無料利用枠の利用期間中に発生した低頻度ストレージ/アーカイブストレージ容量、リクエスト、トラフィックなどの、**標準ストレージ容量以外の**課金項目は、無料の範囲に含まれません。
>- ユーザーの無料利用枠の利用期間中に、違法・禁止行為によるサービス停止、支払い延滞によるサービス停止が発生した場合、無料利用枠を引き続き利用することはできません。無料利用枠を引き続き利用するには、サービスの再開が必要です。

<table>
   <tr>
      <th>料金項目</th>
      <th>課金項目</th>
      <th>無料利用枠を利用可能か</th>
   </tr>
   <tr>
      <td rowspan="5">ストレージ容量料金</td>
      <td>INTELLIGENT_TIERINGストレージ容量</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>標準ストレージ容量</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>低頻度ストレージ容量</td>
      <td rowspan="7">いいえ<br>詳細については<a href="https://intl.cloud.tencent.com/document/product/436/33776">課金項目</a>をご参照ください</td>
   </tr>
   <tr>
      <td>アーカイブストレージ容量</td>
   </tr>
   <tr>
      <td>ディープアーカイブストレージ容量</td>	   
   </tr>
   <tr>
      <td>リクエスト料金</td>
      <td>リクエスト数</td>
   </tr>
   <tr>
      <td>データ取得料金</td>
      <td>データ取得量</td>
   </tr>
   <tr>
      <td rowspan="1">トラフィック料金</td>
      <td>パブリックネットワークダウンストリームトラフィック、CDN back-to-originトラフィック、地域間コピートラフィック、グローバルアクセラレーショントラフィック</td>
   </tr>
   <tr>
	     <td rowspan="1">管理機能料金</td>
       <td>リスト機能料金、検索機能料金、バッチ処理料金、オブジェクトタグ料金</td>
   </tr>
</table>



## 受け取りと照会

ユーザーが[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[COSコンソール](https://console.cloud.tencent.com/cos5)にログインしてCOSサービスをアクティブ化すると、ユーザーアカウント宛てにシステムから自動的に発行されます。無料利用枠はリソースパックの形式で発行されます。

## 有効期間の計算

**無料利用枠有効期間**は、ユーザーがCOSをアクティブにしてから6か月間です。

例えば、ユーザーがCOSをアクティブ化した時間が2019年3月10日 17:13:14であった場合、6か月を180日として計算し、3月10日～9月5日の標準ストレージ容量が無料利用枠の対象となります。

## 決済の順序

ユーザーが無料利用枠を利用していても、それ以外の料金が発生する場合があります。例えばリクエスト料金、トラフィック料金などの基本料金です。このため、請求書の決済時に、システムはケースに応じて異なる決済順序をとります。
- デフォルトでは、システムは**従量課金**方式により決済します。
- ユーザーが標準ストレージ容量の無料利用枠を利用し、リソースパックを購入していない場合、決済の順序は**無料利用枠** > **従量課金**となります。つまり、システムは無料利用枠から優先的に差し引き、無料利用枠を超過した部分は**従量課金**方式により決済します。


## 事例の説明

ユーザーの小雲さんは2019年3月10日にCOSサービスをアクティブ化し、3月16日に60Gの標準ストレージファイルをCOSにアップロードし、3月20日にパブリックネットワークを通じて10Gのデータをダウンロードし、それ以外の時間は他の操作を何も行いませんでした。この場合は次のようになります。

- 小雲さんは有効期間6か月、每月50GBの標準ストレージ容量を獲得しています。
- 2019年3月21日に、パブリックネットワークダウンストリームトラフィック料金として、合計10Gの料金が決済されます。
- 2019年4月1日に標準ストレージ容量料金が決済されます。3月16日～3月31日の期間、毎日無料利用枠を10GB超過しており、16日間で160GBとなります。これを31日で割り、約5.16GBの標準ストレージ容量料金が課金されます。
- 2019年4月初めに、3月にデータをアップロードおよびダウンロードしたことによって発生したリクエスト数料金が決済されます。

2019年4月に、小雲さんは何も操作を行わず、60Gのデータは引き続きCOSに存在します。この場合は次のようになります。

- 2019年5月初めに標準ストレージ容量料金が決済されます。月間ストレージ容量は60Gであり、無料利用枠を超過しているため、**超過した10Gの標準ストレージ容量について追加料金を支払う必要があります**。

> ?上記の事例は、ユーザーが初めてCOSサービスをアクティブ化し、無料利用枠を利用する場合の課金説明です。無料利用枠が期限切れとなった後、どのように料金を計算するかについては、[課金の例](https://intl.cloud.tencent.com/document/product/436/6241)のドキュメントをご参照ください。

## 問題が発生した場合

無料利用枠または請求書にご不明な点がありましたら、[従量課金](https://intl.cloud.tencent.com/document/product/436/10373) のドキュメントを参照し、ご確認ください。
