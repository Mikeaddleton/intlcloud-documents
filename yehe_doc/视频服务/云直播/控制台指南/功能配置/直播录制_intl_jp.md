CSSでは、ライブストリーミングの画面をレコーディングし、ファイルをVODの中に保存する機能を提供しています。VOD経由でレコーディングしたビデオには、ダウンロード、プレビューなどの処理を行うことができます。ここでは、レコーディングテンプレートの作成、バインド、バインド解除、修正および削除の方法をご紹介します。
レコーディングテンプレートの作成には次の2つの方法があります。

- CSSコンソールによるレコーディングテンプレートの作成。具体的な操作手順は、[レコーディングテンプレートの作成](#C_record)をご参照ください。
-  APIによるレコーディングテンプレートの作成。具体的なパラメータ、サンプル、説明については、 [レコーディングテンプレートの作成](https://intl.cloud.tencent.com/document/product/267/30845)をご参照ください。

## 注意事項
- レコーディングしたビデオファイルはデフォルトで[VOD](https://console.cloud.tencent.com/vod/overview) コンソールに保存されます。よって事前にVODのサービスをアクティブ化しておくことを推奨します。詳細については、[VODクイックスタート](https://intl.cloud.tencent.com/document/product/266/8757)をご参照ください。
- レコーディング機能を有効にした後、VODサービスが正常な使用状態にあることを確認してください。VODサービスが非アクティブ状態またはアカウントの支払い延滞によりサービス停止になるなどの状況が起きた場合は、ライブストリーミングに影響して、レコーディングができなくなります。この期間はレコーディングファイルとレコーディングの費用は発生しません。
- ライブストリーミングの過程では、レコーディング終了後5分前後で対応するファイルを取得できます。例えば、あるライブストリーミングを12:00からレコーディング開始、12：30にレコーディング終了とした場合は、12:35前後に12:00 - 12:30の対応するフィルムを取得でき、後はこのように類推します。
- 音声/ビデオファイル形式（FLV/MP4/HLS）のコーディックタイプのサポート制限により、ビデオコーディックのタイプはH.264をサポートし、音声のコーディックのタイプはAACをサポートしています。
- レコーディングテンプレートの作成完了後、プッシュドメイン名へのバインドを行います。関連ドキュメントについては、 [レコーディング設定](https://intl.cloud.tencent.com/document/product/267/34224)をご参照ください。バインド完了の約5分 - 10分後に有効となります。
- 発行されるレコーディングファイルの命名ルールについてお知りになりたい場合は、[レコーディングテンプレートパラメータ-VodFileName](https://intl.cloud.tencent.com/document/product/267/30767)をご参照ください。
- テンプレートのバインド、修正、バインド解除はいずれも更新後のライブストリーミングにのみ影響し、すでにライブストリーミング中にあるストリームは影響を受けません。ライブストリーミング中のストリームが新しいルールを使用するには、一度切断して再度プッシュする必要があります。
- ミクスストリーミングのレコーディングは、レコーディングファイルエラーが発生し、通常の視聴と再生に影響を与えるため、中国内地（大陸）とグローバル/中国香港・マカオ・台湾のライブミクスストリーミングをサポートしていません。



##  前提条件
- Tencent CSSサービスをアクティブ化し、[プッシュドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済みであること。
- [VODサービス](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD)をアクティブ化していること。

[](id:C_record)
## レコーディングテンプレートの作成
1. CSSコンソールにログインし、**機能設定** > [**CSSレコーディング**](https://console.cloud.tencent.com/live/config/record)に進みます。
2. **レコーディングテンプレート作成**をクリックしてテンプレート情報を設定します。以下の設定を行います。
![](https://main.qcloudimg.com/raw/ccf133a64c38ce579a9fd91e37514193.png)

<table>
   <thead><tr><th width="20%" colspan=2>設定項目</th><th>設定の説明</th></tr></thead>
   <tbody><tr>
   <tr>
   <td colspan=2>テンプレート名</td>
   <td>CSSレコーディングのテンプレート名。カスタマイズ可能です（中国語、英語、数字、「_」、「-」のみ対応）。</td>
   </tr><tr>
   <td colspan=2>テンプレートの説明</td>
   <td>CSSレコーディングのテンプレートの概要説明。カスタマイズ可能です（中国語、英語、数字、「_」、「-」のみ対応）。</td>
   </tr><tr>   
   <td rowspan=2 width="10%">コンテンツのレコーディング</td>
   <td width="20%">オリジナルストリームのレコーディング</td> 
   <td><ul style=margin:0>ビデオのレコーディングは、ライブストリーミングのオリジナルビットレートを対象としてレコーディングします。デフォルトではオリジナルストリームをレコーディングします。</ul></td>
   </tr><tr>
   <td>指定されたトランスコードストリームのレコーディング</td>
   <td> 指定されたトランスコードストリームのレコーディングをクリックすると、設定済みのトランスコードテンプレートを選択するか、テンプレート名をクリックしてトランスコードテンプレート設定の変更へ移動できます。該当の設定を選択すると、プッシュストリーム後にトランスコードテンプレートidに応じて、自動でトランスコードを開始してレコーディングを行います。トランスコードテンプレートが誤って削除された場合は、オリジナルストリームに応じてレコーディングされます。</td>
   </tr><tr>
   <td colspan=2>レコーディング形式</td>
   <td>ビデオレコーディングの出力形式にはHLS、MP4、FLV、AACの4種類があります。そのうちAACはオーディオのみのレコーディングです。</td>
   </tr>
   </tbody></table>
>! 
>- 指定されたトランスコードストリームのレコーディングにおいて、オーディオのみのトランスコードテンプレートを選択した場合、レコーディング形式はオーディオ形式のみ選択できます。
>- トランスコードストリームをレコーディングするには、まずトランスコードタスクを開始する必要があり、トランスコード料金が追加で発生します。 同一のトランスコードテンプレートを使用して再生する場合、重複して課金されることはありません。
3. レコーディングコンテンツを選択し、必要なレコーディング形式にチェックを入れると、該当する形式の設定インターフェースがポップアップ表示され、同時に設定する1つまたは複数のレコーディング形式を選択できます。以下の設定を行ってください。
![](https://main.qcloudimg.com/raw/74a4ac0636c59ff69c23437e72189567.png)

<table>
   <thead><tr><th width="27%" colspan=2>設定項目</th><th>設定の説明</th></tr></thead>
   <tbody><tr>
      <tr>
      <td colspan=2>レコーディングファイル1つあたりの長さ（分）</td>
      <td><ul style="margin-bottom:0px">
          <li>HLS形式でレコーディングするファイル1つあたりのレコーディング時間は無制限です。レコーディング継続の待機時間を超えた場合は、ファイルを新規作成し、レコーディングを継続します。</li>
          <li>MP4、FLVまたはAAC形式でレコーディングするファイル1つあたりの長さ制限は1分～120分です。</li>
          </ul></td>
      </tr><tr>
      <td colspan=2>レコーディング継続の待機時間（秒）</td>
      <td>HLS形式のファイルのみ、プッシュ中断のレコーディング継続をサポートし、レコーディング継続の待機時間を1s～1800sに設定できます。</td>
      </tr><tr>
      <td colspan=2>保存時間（日）</td>
      <td>レコーディングファイル1つあたりの最大保存時間は1500日で、ファイル保存時間が0の場合は永久保存です。<b>永続ストレージ</b> または <b>指定期間</b>を選択できます。</td>
      </tr><tr>
      <td colspan=2>オンデマンドアプリケーション/カテゴリーの指定</td>
      <td>VODの指定 <a href="https://console.cloud.tencent.com/vod/app-manage">するサブアプリケーション</a>のオンデマンドカテゴリーにレコーディングする機能をサポートしています。デフォルトではアカウントのメインアプリケーションにレコーディングされ、書き込みステータスが有効になっているサブアプリケーションにのみ対応できます。</td>
      </tr><tr>
      <td rowspan=2 width="12%">高度な設定</td>
      <td>ビデオストレージポリシー</td> 
      <td><ul style=margin:0><li>レコーディングしたビデオを通常業務で再生する必要がある場合、標準ストレージでニーズを満たすことができ、デフォルトは標準ストレージになります。</li><li>VODにレコーディングしたメディアアセットのクールダウンをサポートします。レコーディングファイルに頻繁にアクセスする必要がない場合は、クールダウン機能を使用して、低頻度アクセスと長期保存を可能にすることができます。</li></ul></td>
      </tr><tr>
      <td>オンデマンドタスクフロー処理</td>
      <td><b>バインドするタスクフローの選択</b>をクリックすると、オンデマンドサブアプリケーションで作成されたタスクフローをバインドするか、現在のオンデマンドタスクフロー選択インターフェースでタスクフロー名をクリックしてVODコンソールに移動し、タスクフローの設定を追加/変更するかを選択できます。バインドに成功すると、レコーディングファイルの発行後にオンデマンドタスクフローテンプレートが実行され、対応する<a href="https://tcloud-doc.isd.com/document/product/266/2838">VOD料金</a>が発生します。</td>
      </tr>
      </tbody></table>

>! ビデオストレージポリシーのうち、
>- **標準ストレージ**を選択した場合、現在選択されているアプリケーションでクールダウンポリシーが有効になっていれば、レコーディングファイルは最初に標準ストレージファイルを発行し、次にクールダウンポリシーに従ってクールダウンを実行します。ここをクリックすると、[ポリシーを確認](https://console.cloud.tencent.com/vod/inactivation)できます。
**低頻度ストレージ**を選択するときに、現在選択されているアプリケーション/カテゴリーはクールダウンポリシーが有効になっている場合、レコーディングファイルは低頻度ストレージファイルを直接発行してから、VODクールダウンポリシーを実行するかどうか判断します。
4. **保存**をクリックすれば完了です。

[](id:conect)
## ドメイン名のバインド
1. CSSコンソールにログインし、**機能設定** > [**CSSレコーディング**](https://console.cloud.tencent.com/live/config/record)に進みます。
    - **ドメイン名の直接的関連付け：**左上にある**ドメイン名のバインド**をクリックします。
    ![](https://main.qcloudimg.com/raw/bcb6c5da46a3455f94d441134e49825a.png)
    - **新規レコーディングテンプレート作成完了後のドメイン名関連付け：**[レコーディングテンプレートの作成](#C_record)の完了後、プロンプトボックスの中の**ドメイン名のバインドに進む**をクリックします。
    ![](https://main.qcloudimg.com/raw/7f26a83d95d0f08ceda1b10e93e30389.png)
2. ドメイン名バインドのウィンドウの中で、バインドしたい**レコーディングテンプレート**および**プッシュドメイン名**を選択し、**OK**をクリックすればバインドが完了します。
![](https://main.qcloudimg.com/raw/a9411818457b4e708fd624f970d92ab6.png)

> ? **追加**をクリックして現在のテンプレートに複数のプッシュドメイン名をバインドする機能をサポートしています。

[](id:unite)
## バインドの解除
1. CSSコンソールにログインし、**機能設定** > [**CSSレコーディング**](https://console.cloud.tencent.com/live/config/record)に進みます。
2. すでに関連付けしたドメイン名のレコーディングテンプレートを選択し、バインドを解除したいドメイン名を選択して右側の**バインド解除**をクリックします。
   ![](https://main.qcloudimg.com/raw/f7071a4b4f9297124b460ffebcba64d3.png)
3. 現在関連付けられているドメイン名のバインドを解除するかどうかを確認して、**OK**をクリックすればバインドが解除されます。
    ![](https://main.qcloudimg.com/raw/a666387f882584860eaf2c229c2b4769.png)

>? 
>- レコーディングテンプレートのバインド解除後、ライブストリーミング中のストリームには影響しません。
>- バインド解除を有効にしたい場合は、バインド解除後にストリームを停止して再度ライブストリーミングをプッシュしてください。新規ライブストリーミングにレコーディングファイルが生成されなくなります。


[](id:change)
## テンプレートの修正
1. **機能設定** > [**CSSレコーディング**](https://console.cloud.tencent.com/live/config/record)に進みます。
2. 作成済みのレコーディングテンプレートを選択し、右側の**編集**をクリックすれば、テンプレートの情報を変更でき、**保存**をクリックすると完了します。
![](![img](https://main.qcloudimg.com/raw/68f4dd1a6452a3e97e7ff4dea6493d7b.png)

[](id:delete)
## テンプレートの削除
1. CSSコンソールにログインし、**機能設定** > [**CSSレコーディング**](https://console.cloud.tencent.com/live/config/record)に進みます。
2. 作成済みのレコーディングテンプレートを選択し、右上の**削除**をクリックします。
3. 現在のレコーディングテンプレートを削除するかどうかを確認し、**OK**をクリックすれば削除が完了します。
![](https://main.qcloudimg.com/raw/c7c3e300488ba332b84bfd61da0fb999.png)

>! 
>- テンプレートがすでにバインドされている場合は、先に[バインドの解除](#unite)を行ってから、削除操作を行うことができます。
>- コンソールのレコーディングテンプレートの管理はドメイン次元となり、現在はインターフェース関連付けの作成ルールを取り消しすることができません。レコーディング管理インターフェースの関連付けによってストリームを指定している場合は、[レコーディングルールの削除](https://intl.cloud.tencent.com/document/product/267/30843)を呼び出して、関連付けを解除する必要があります。 


## 関連する操作
**ドメイン次元のレコーディングテンプレートのバインド**と**バインド解除**の具体的な操作および関連説明については、[レコーディング設定](https://intl.cloud.tencent.com/document/product/267/34224)をご参照ください。


## 関連する質問
[](id:que1)
#### CSSレコーディング後に生成されるビデオ名はどのようなルールで生成されますか？
コンソールで作成したレコーディングテンプレートにより、コールバック後に生成されるレコーディングファイルは、デフォルトでは接合方式による命名となっています。形式は次のとおりです。
`{StreamID}*{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}*{EndYear}-{EndMonth}-{EndDay}-{EndHour}-{EndMinute}-{EndSecond} `

**このうち：**

| プレースホルダー             | 意味          |
| ------------------ | ------------- |
| {StreamID}         | ストリームID          |
| {StartYear}        | 開始時間-年   |
| {StartMonth}       | 開始時間-月   |
| {StartDay}         | 開始時間-日   |
| {StartHour}        | 開始時間-時 |
| {StartMinute}      | 開始時間-分 |
| {StartSecond}      | 開始時間-秒   |
| {EndYear}          | 終了時間-年   |
| {EndMonth}         | 終了時間-月   |
| {EndDay}           | 終了時間-日   |
| {EndHour}          | 終了時間-時 |
| {EndMinute}        | 終了時間-分 |
| {EndSecond}        | 終了時間-秒   |
