## Demo体験
<input type="button" value="Windows版" style="height: 30px;width: 150px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;margin-right:10px;"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-windows-latest.zip')" />

<input type="button" value="MacOS版" style="height: 30px;width: 150px;margin-top: 5px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education-v2/TRTCEducationElectron-mac-latest.zip')" />

## デモンストレーション
すでに作成してあるAppインストールパッケージをダウンロード、インストールして、リアルタイムインタラクティブ授業の機能を体験することができます。基本的なオーディオビデオ通話、画面共有、ホワイトボード、チャットなどの基本機能を提供するだけでなく、全員のマイクミュート、学生の挙手による発言申請、先生の学生への発言要請、点呼、サインインなどといった高度な機能の提供も実現しました。


## リアルタイムインタラクティブ授業クイックスタートのソースコード
[](id:step1)
### ステップ1：アプリケーションの作成、SDKAppIDとキーの取得
すでにTRTCのアプリケーションを作成している場合は、このステップをスキップし、以前作成したアプリケーションのSDKAppIDとキーを直接使用することができます。

1. TRTCコンソールにログインし、**開発支援** > **[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択し、**アプリケーションの作成**タブで`TestTRTC`などのアプリケーション名を入力して、**作成**ボタンをクリックします。  
![](https://qcloudimg.tencent-cloud.cn/raw/dfb1acca0137cd30d5168c3d9d72aa13.png)
2. **ソースコードのダウンロード**タブをスキップし、**次のステップ**ボタンを直接クリックして**設定の変更**タブに進み、次のページに表示されたSDKAppIDとキーを以後のステップで使用できるよう、記録します。
![](https://qcloudimg.tencent-cloud.cn/raw/ca5da75be8285ead342e06971229680e.png)

[](id:step2)
### ステップ2：Instant Messagingの設定
>?リアルタイムインタラクティブ授業はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期してアクティブ化することができます。 IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

1. **関連するクラウドサービス**メニューに進み、下図の**IMアプリケーション**をクリックしてIMアプリケーション管理ページにジャンプします。
    ![](https://qcloudimg.tencent-cloud.cn/raw/14e4c3b097ecadb046330975dbec6bd0.png)

2. 先ほど作成したアプリケーションを見つけてクリックするとアプリケーション管理ページに進み、下図のように表示されます。
    ![](https://qcloudimg.tencent-cloud.cn/raw/50aa612285befcfa14562923622cad6d.png)

3. メニューの**機能設定** > **ログインとメッセージ**を開くと、下図のように表示されますので、**ログイン設定**エリアの**編集**リンクをクリックし、**Web端末の同時オンライン可能数**を2以上の値に設定します（現在このアプリケーションで最もニーズが多いのは同時に2つのWeb IMインスタンスへのログインで、引き続き使用する際の設定の追加が可能です）。

   ![](https://qcloudimg.tencent-cloud.cn/raw/2385858860a8f12091eab619b313eaec.png)


[](id:step3)
### ステップ3：実行環境の準備
このコードプロジェクトの実行はnode.jsとyarnに依存します。

1. **node.jsのインストール**
[node.js](https://nodejs.org/en/download/) は14.16.0以降のバージョンの使用をお勧めします。インストール完了後、コマンドライン端末で以下のコマンドを実行してnode.jsのバージョンを確認してください。
```
node --version
```
2. **yarnのインストール**
 - node.jsのバージョンが16.10より前の場合は、コマンドライン端末で以下のコマンドを実行して[yarn](https://yarnpkg.com/getting-started/install)をインストールします。
```
npm i -g corepack
```
 - node.jsのバージョンが16.10以降の場合は、コマンドライン端末で以下のコマンドを実行してyarnをインストールします。
```
corepack enable
```
>!Window10、11で権限不足のエラーメッセージが表示されたときは、 管理者ロールによりcmdで実行してみてください。



[](id:step4)
### ステップ4：コードクローンプロジェクト

直接[コードのダウンロード](https://github.com/TencentCloud/trtc-education-electron)ができ、解凍後にコードディレクトリ`trtc-education-electron`、または [git](https://git-scm.com/downloads) ツールを使用したコードクローンプロジェクトに進みます。gitツールを使用したコードクローンプロジェクトでは、コマンドライン端末で以下のコマンドを実行してください。

```
git clone https://github.com/TencentCloud/trtc-education-electron.git

cd trtc-education-electron
```

[](id:step5)
### ステップ5：SDKAppIDとキーの設定
1. `src/main/config/generateUserSig.js`ファイルを見つけて開きます。
2. 身分認証発行用のユーザー署名UserSigに使用するため、`generateUserSig.js`ファイルの関連パラメータを設定します。
   - SDKAPPID：デフォルトは0。 [ステップ1](#step1)で作成したアプリケーションのSDKAppIDを設定してください。
   - SECRETKEY：デフォルトは空文字列。 [ステップ1](#step1) で作成したアプリケーションのキーを設定してください。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step6)
### ステップ6：開発モードの実行
コマンドライン端末で、コードディレクトリ`trtc-education-electron`に進み、以下のコマンドを実行します。
```
yarn

yarn start
```
>!
>- 初めてyarnコマンド実行の依存関係をインストールする際、Window10、Window11で権限不足のエラーメッセージが表示された場合は、管理者ロールによりcmdで一度実行してみてください。その後は一般ユーザーロールによりcmdまたはVisual Studio Code、WebStormといった統合開発ツール付属の端末で実行することができます。
>- 依存関係のインストール中に、Electronのダウンロードが遅い、またはスタックするなどの問題が発生した場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us) を参照して問題を解決できます。

[](id:step7)
### ステップ7：インストールパッケージの作成、実行
コマンドライン端末で、コードディレクトリ`trtc-education-electron`に進み、以下のコマンドを実行してインストールパッケージを作成します。作成したインストールパッケージは`trtc-education-electron/build/release`ディレクトリにあり、インストールの実行が可能です。

```
yarn package
```

>!Mac PCを使用したMacインストールパッケージの作成、Windows PCを使用したWindowsインストールパッケージの作成のみ可能です。


## 技術的なお問い合わせ
詳細については、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)にご連絡をいただくか、colleenyu@tencent.comにメールでご連絡ください。

## 参考ドキュメント

- [SDK APIマニュアル](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK更新ログ](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demoソースコード](https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTCSimpleDemo)
- [API Exampleソースコード](https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example)
- [Electronについてのよくあるご質問](https://intl.cloud.tencent.com/document/product/647/43093)
