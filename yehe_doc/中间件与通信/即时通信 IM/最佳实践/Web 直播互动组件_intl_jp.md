## まえがき

ここでは、[IM](https://intl.cloud.tencent.com/product/im)と[TRTC](https://intl.cloud.tencent.com/product/trtc)を統合したWebRTCライブストリーミングインタラクションコンポーネント（UIを含む）についてご紹介いたします。

Instant Messaging（IM）は、さまざまなニーズとシナリオに対応する一連のソリューションを提供します。IMの強力なチャットルームインタラクション機能、リレーションシップチェーンホスティング、サードパーティのコールバック機能は、チャットインタラクション、オーディエンス管理、インタラクション抽選といったライブストリーミングシナリオのニーズを完全に満たします。また、開発者のライブストリーミングに対する低遅延要件や高速アクセスに対するニーズに配慮し、IMはTRTCと連携して、UIを含むWeb端末のインタラクティブライブストリーミング・プッシュプルストリーミングコンポーネントであるTUIPusherとTUIPlayerをリリースしました。

今回リリースされた[TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher)と[TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer)コンポーネントは、視聴者リスト、チャットインタラクション、美顔、画面共有などの機能をカバーしています。展開してすぐに使用でき、主なデスクトップブラウザと互換性があります。TUIPusherとTUIPlayerの機能デモンストレーションについては、下図をご参照ください。また、ユーザー管理システムとルーム管理システムを組み合わせており、[TUIPusher体験リンク](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html)および[TUIPlayer体験リンク](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html)を提供しています。




## 機能の説明

### TUIPusherプッシュコンポーネント

- カメラとマイクからのストリームの収集とプッシュをサポート
  - 必要に応じてビデオパラメータ（フレームレート、解像度、ビットレート）を設定
  - 美顔の起動とビデオ美顔パラメータの設定をサポート
- 画面共有ストリームの収集とプッシュをサポート
- Tencent Real-Time Communicationバックエンドへのプッシュ、Tencent Cloud CDNへのプッシュをサポート
- オンラインチャットルームをサポートし、オンライン視聴者とのインタラクティブなチャットを実現
- 視聴者リストの取得、オンライン視聴者のミュート操作の実行をサポート

### TUIPlayerプルコンポーネント

- オーディオビデオストリーミングと画面共有ストリーミングの同時再生をサポート
- オンラインチャットルームをサポートし、キャスターおよびその他視聴者のインタラクティブなチャットを実現
- 超低遅延ライブストリーミング（300msの遅延）、ライブイベントストリーミング（1000ms以下の遅延）、標準ライブストリーミング（超高速同時視聴をサポート）の3種類のプル回線をサポート


## アクセス方法

### 注意事項

- TUIPusher&TUIPlayerは、Tencent Cloud TRTCとInstant Messagingサービスをベースに開発されています。アカウントと認証を再利用するためには、TRTCアプリケーションとIMアプリケーションのSDKAppIDが一致している必要があります。
- UserSigをローカルで計算する方式は、ローカルでの開発とデバッグのみに使用されます。SECRETKEYが漏洩すると、攻撃者がTencent Cloudトラフィックを盗用する可能性があるので、オンラインで直接発行しないでください。UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

[](id:step1)

### ステップ1：Tencent Cloudサービスのアクティブ化

<dx-tabs>
::: 方法1：インスタントメッセージ\sIMの場合
#### 手順1：IMアプリケーションの作成

1. [IMコンソール](https://console.cloud.tencent.com/im)にログインし、**新しいアプリケーションの作成**をクリックするとダイアログボックスがポップアップします。
   ![](https://main.qcloudimg.com/raw/b2acb7f79117f0828928e13a17ea9a6a.png)
2. 自分のアプリケーション名を入力して、**確定**をクリックすると作成が完了します。
   ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
3. [IMコンソール](https://console.cloud.tencent.com/im)の概要画面で、新規作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、有効期限を確認することができます。SDKAppID情報を記録してください。

#### 手順2：IMキーを取得してTRTC Video Serviceをアクティブにする

1. [IMコンソール](https://console.cloud.tencent.com/im)の概要ページで、自分で作成を完了したIMアプリケーションをクリックして、直ちにそのアプリケーションの基本設定ページにリダイレクトします。**基本情報**領域で、**キーの表示**をクリックして、キー情報をコピーし保存します。
   ![](https://main.qcloudimg.com/raw/610dee5720e94e324a48b44f4728816a.png)

>!キー情報を適切に保管して、漏えいしないようにしてください。

2. そのアプリケーションの基本構成ページで、TRTCサービスをアクティブ化します。
   ![](https://main.qcloudimg.com/raw/8fb2940618dfb8b7ea06eecd62212468.png)

:::
::: 方法2：TRTCの場合

#### 手順1：TRTCアプリケーションの作成

1. [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/register)を行い、[TRTC](https://console.cloud.tencent.com/trtc)と[IM](https://console.cloud.tencent.com/im)サービスをアクティブ化します。
2. [TRTCコンソール](https://console.cloud.tencent.com/trtc) で、**アプリケーション管理>アプリケーションの作成** をクリックし、新たなアプリケーションを作成します。
   ![アプリケーションの作成](https://main.qcloudimg.com/raw/871c535f4b539ad7791f10d57ef0a9f3.png)

#### ステップ2： TRTCキー情報の取得

1. **アプリケーション管理>アプリケーション情報**でSDKAppID情報を取得します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/4efba95edf4073238420a40ec9a6b3b3.png)
2. **アプリケーション管理>クイックマスター**でアプリケーションのsecretKey情報を取得します。
   ![](https://main.qcloudimg.com/raw/8ec16ab9cab85e324a347dea511f7e4e.png)

>?
>
>- TRTCアプリケーションを初めて作成するTencent Cloudアカウントは、10000分間のオーディオビデオリソース無料トライアルパッケージを受け取ることができます。
>- TRTCプリケーションを作成すると、同じSDKAppIDのIMアプリケーションが自動的に作成され、 [IMコンソール](https://console.cloud.tencent.com/im)でこのアプリケーションのパッケージ情報を設定することができます。

:::
</dx-tabs>

[](id:step2)
### ステップ2：プロジェクトの準備

1. [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web)でTUIPusher & TUIPlayerコードをダウンロードします。
2. TUIPusher & TUIPlayerのためにインストールして依存します。
   ```bash
   cd Web/TUIPusher
   npm install
   
   cd Web/TUIPlayer
   npm install
   ```
3. sdkAppIdとsecretKeyを`TUIPusher/src/config/basic-info-config.js`、`TUIPlayer/src/config/basic-info-config.js`設定ファイルに入力します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/2367f9c25773bc5d5de9db00d0962f06.png)
4. ローカル開発環境でTUIPusher＆TUIPlayerを実行します。
   ```bash
   cd Web/TUIPusher
   npm run serve
   
   cd Web/TUIPlayer
   npm run serve
   ```
5. `http://localhost:8080`と`http://localhost:8081`を開き、TUIPusherとTUIPlayer機能を体験することができます。
6. `TUIPusher/src/config/basic-info-config.js`、`TUIPlayer/src/config/basic-info-config.js`設定ファイル中のルーム，キャスターおよび視聴者などの情報を変更することができます。**TUIPusherとTUIPlayerのルーム情報、キャスター情報を一致させてください**。
>!
>
> - 上記設定が完了すると、TUIPusher & TUIPlayerを使用して超低遅延ライブストリーミングを実行することができます。ライブイベントストリーミングと標準ライブストリーミングをサポートする必要がある場合は、引き続き[ステップ3：Relayed Live Streaming](#step3)をご参照ください。
> - UserSigをローカルで計算する方法は、ローカルの開発とデバッグにのみ使用されます。`SECRETKEY`が漏えいすると、攻撃者がTencent Cloudのトラフィックを盗用する可能性があるので、ネット上にそのまま公開しないでください。
> - UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。


[](id:step3)
### ステップ3：Relayed live streaming

TUIPusher&TUIPlayerによって実装されるライブイベントストリーミングと標準ライブストリーミングはTencent Cloud[CSSサービス]（https://intl.cloud.tencent.com/document/product/267）に依存しているため、ライブイベントストリーミングと標準ライブストリーミング回線をサポートするには、Relayed Push機能を有効にする必要があります。

1. [**TRTCコンソール**](https://console.cloud.tencent.com/trtc) で現在使用中のアプリケーションのRelayed Push設定を有効にします。必要に応じてRelayed Push用指定ストリームまたはGlobal Auto-relayを起動することができます。
   ![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
2. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)ページで独自の再生ドメイン名を追加します。具体的な内容は[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)をご参照ください。
3. `TUIPlayer/src/config/basic-info-config.js`設定ファイルで再生ドメイン名を設定します。

上記設定が完了すると、TUIPusher & TUIPlayerがサポートする超低遅延ライブストリーミング、ライブイベントストリーミング、標準ライブストリーミングの全機能を体験できます。

[](id:step4)
### ステップ4：本番環境アプリケーション

TUIPusher & TUIPlayerを本番環境アプリケーションに使用する場合は、TUIPusher & TUIPlayerにアクセスすることに加え、次の手順を実行する必要があります。

- ユーザーID、ユーザー名、ユーザープロフィール画像などを含む製品ユーザー情報を管理するためのユーザー管理システムを作成します。
- ライブストリーミングルームID、ライブストリーミングルーム名、ライブストリーミングルームのホスト情報などを含む製品のライブストリーミングルーム情報を管理するためのルーム管理システムを作成します。
- サーバーがUserSigを発行します。

> !
>
> - ここでのUserSigの発行方法は、クライアントが入力したsdkAppIdとsecretKeyに基づきuserSigを発行する方法です。この方法で発行されるsecretKeyは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この方法はローカルのTUIPusher & TUIPlayerクイックスタート機能デバッグの実行のみに適しています**。
> - UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、アプリケーションから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

- `TUIPusher/src/pusher.vue`、`TUIPlayer/src/player.vue`ファイルを参照し、ユーザー情報、ライブストリーミングルーム情報、SDKAppId、UserSigなどのアカウント情報をvuexのstoreに送信し、グローバルストレージを実行すると、プッシュプルストリーミングする2つのクライアントの全機能をクイックスタートすることができます。

## 関連する質問

1. Web端末での美容機能の実現方法
   [美顔を有効にする](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)をご参照ください。

2. Web端末での画面共有の実現方法。
   [画面共有](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)をご参照ください。

3. Web端末でのクラウドレコーディングの実現方法。
   クラウドレコーディングを有効にするには、[クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426)をご参照ください 。
   【クラウドレコーディング】> 【指定ユーザーレコーディング】を有効にすると、Web端末が[TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)インターフェース呼び出し時にuserDefineRecordIdパラメータを渡すことによってレコーディングを開始できます。

4. Web端末でのCDNへのプッシュの実現方法。
   Web端末でのCDNへのプッシュについては、[CDNへのプッシュの実現](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html)をご参照ください。


## 注意事項

###  プラットフォームのサポート

| オペレーションシステム（OS） | ブラウザタイプ                   | ブラウザ最低バージョン要件 | TUIPlayer | TUIPusher | TUIPusher画面共有           |
| -------- | ---------------------------- | ------------------ | --------- | --------- | ---------------------------- |
| Mac OS   | デスクトップ版Safariブラウザ         | 11+                | サポートあり      | サポートあり      | サポートあり（Safari13以降のバージョンが必要）  |
| Mac OS   | デスクトップ版Chromeブラウザ         | 56+                | サポートあり      | サポートあり      | サポートあり（Chrome72以降のバージョンが必要）  |
| Mac OS   | デスクトップ版Firefoxブラウザ        | 56+                | サポートあり      | サポートあり      | サポートあり（Firefox66以降のバージョンが必要） |
| Mac OS   | デスクトップ版Edgeブラウザ           | 80+                | サポートあり      | サポートあり      | サポートあり                         |
| Mac OS   | デスクトップ版WeChat Embedded Webページ           | -                  | サポートあり      | サポートなし    | サポートなし                       |
| Mac OS   | デスクトップ版WeCom Embedded Webページ       | -                  | サポートあり      | サポートなし    | サポートなし |
| Windows  | デスクトップ版Chromeブラウザ         | 56+                | サポートあり      | サポートあり      | サポートあり（Chrome72以降のバージョンが必要）  |
| Windows  | デスクトップ版QQブラウザ（クイックコア）  | 10.4+              | サポートあり     | サポートあり      | サポートなし                       |
| Windows  | デスクトップ版Firefoxブラウザ        | 56+                | サポートあり      | サポートあり      | サポートあり（Firefox66以降のバージョンが必要） |
| Windows  | デスクトップ版Edgeブラウザ           | 80+                | サポートあり      | サポートあり      | サポートあり                         |
| Windows  | デスクトップ版WeChat Embedded Webページ           | -                  | サポートあり      | サポートなし    | サポートなし                       |
| Windows  | デスクトップ版WeCom Embedded Webページ       | -                  | サポートあり      | サポートなし    | サポートなし                       |

### ドメイン名要件

ユーザーのセキュリティ、プライバシーなどの問題を考慮し、ブラウザはHTTPSプロトコルでしかTUIPusher & TUIPlayerの全機能を正常に使用できないようにウェブページを制限しています。本番環境のユーザーがTUIPusher & TUIPlayerの全機能にスムーズにアクセスし体験できるようにするには、HTTPSプロトコルを使用してオーディオビデオアプリケーションページにアクセスしてください。

>! ローカル開発には、`http：// localhost`プロトコルを使用してアクセスできます。

URLドメイン名およびプロトコルのサポート状況については、以下の表をご参照ください。

| ユースケース     | プロトコル               | TUIPlayer | TUIPusher | TUIPusher画面共有 | 備考 |
| ------------ | ------------------ | --------- | --------- | ------------------ | ---- |
| 本番環境     | HTTPSプロトコル         | サポートあり      |  サポートあり         | サポートあり               | 推奨 |
| 本番環境     | HTTPプロトコル          | サポートあり      | サポートなし       | サポートなし             | -    |
| ローカル開発環境 | `http://localhost` | サポートあり      | サポートあり      | サポートあり               | 推奨 |
| ローカル開発環境 | `http://127.0.0.1` | サポートあり      | サポートあり      | サポートあり               | -    |
| ローカル開発環境 | `http://[ローカルマシンIP]`  | サポートあり      | サポートなし    | サポートなし             | -    |

### ファイアウォールの制限

TUIPusher & TUIPlayerは次のポートに依存してデータ送信を実行しています。これらのポートをファイアウォールのホワイトリストに追加してください。

- TCPポート：8687
- UDPポート：8000、8080、8800、843、443、16285
- ドメイン名：qcloud.rtc.qq.com

## 結び

今後のイテレーションで、ここでご紹介したWeb端末のプッシュプルコンポーネントは、iOS、Andriodなどの各端末と徐々に接続し、Web端末において視聴者のマイク接続機能、高度な美顔、カスタムレイアウト、マルチプラットフォームへのプッシュ転送、画像・テキスト・音楽などのアップロード機能を実装します。eコマースライブストリーミングのシーンでは、[IM](https://intl.cloud.tencent.com/product/im)を使用して、モールへの出品・削除、パスワード抽選、Q&A抽選など、多様な遊び方を実装する予定です。ぜひご利用いただき、貴重なご意見をお聞かせください。

ご要望やご意見がありましたら、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)までお願いいたします。

