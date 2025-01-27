## 概要
WebShellはTencent Cloudに推薦されたログイン方式です。お客様のロカールOSはWindows、Linux、またはMac OSのどちらでも、インスタンスがパブリックIPを購入している限り、WebShellによりログインすることができます。このドキュメントは、標準ログイン方式（WebShell）を利用してLinux インスタンスにログインする方法について説明します。
WebShellの利点は下記の通り：
- コピー＆ペーストのショートカットキーをサポートします。
- マウスのスクロールをサポートします。
- 中国語入力をサポートします。
- セキュリティが高い、ログインするたびにパスワードまたはキーを入力する必要があります。

## 認証方式

**パスワード**または**キー**です。

## 前提条件[](id:Prerequisites)

- Linuxインスタンスにログインするための管理者のアカウントとパスワード（またはキー）を取得済みであること。
 - インスタンス作成時に、システムによるパスワードのランダム発行を選択した場合は、[サイト内メッセージ](https://console.cloud.tencent.com/message)にアクセスして取得してください。
 - ログインパスワードを設定済みの場合は、そのパスワードを使用してログインしてください。パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
 - インスタンスにキーをバインドしている場合、そのキーを使ってログインすることができます。キーに関する詳細については、[SSHキー](https://intl.cloud.tencent.com/document/product/213/6092)をご参照ください。
- お客様のCVMインスタンスはパブリックIPをすでに購入しており、インスタンスにバインドしたセキュリティグループの中で、送信元がWebShellのプロキシIPとなるリモートログインポート（デフォルトは22）を開放しています。
 - クイック設定経由でCVMを購入した場合、デフォルトの状態ではアクティブになっています。
 - カスタム設定経由でCVMを購入した場合は、[Linux CVMへのSSHリモート接続の許可](https://intl.cloud.tencent.com/document/product/213/32369)を参照して、手動でアクセスを許可してください。

## 操作手順

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
<dx-tabs>
::: リストビュー
下図に示すように、ログインしたいLinux CVMを見つけ、右側にある**ログイン**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: タブビュー
下図に示すように、ログインしたいLinux CVMタブを選択し、**ログイン**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>

3. 下図に示すように、開いた「標準ログイン｜Linuxインスタンス」ウィンドウで、実際のニーズに応じて**パスワードでログイン**または**キーでログイン**方式のいずれかを選択し、ログインします。
![](https://main.qcloudimg.com/raw/9c321ad519c8f993c1f768e56fca0ab1.png)
以下の説明を参照して、ログインに必要な情報を入力してください。
 -  **ポート**：デフォルトは22です。必要に応じて入力してください。
 - **ユーザー名**：Linuxインスタンスのデフォルトのユーザー名はroot（Ubuntuシステムインスタンスのデフォルトのユーザー名はubuntu）です。必要に応じて入力してください。
 -  **パスワード**：[前提条件](#Prerequisites)のステップで取得したログインパスワードを入力します。
 - **キー**：バインドしたインスタンスのキーを選択します。
4. **ログイン**をクリックすると、Linuxインスタンスにログインできます。
ログインに成功すると、下図に示すように、WebShellインターフェースに以下のプロンプトが表示されます。
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)

## 後続の操作

CVMにログインした後、個人用Webサイトまたはフォーラムを構築したり、その他の操作を実行したりできます。関連操作については、下記をご参照ください：　　
- [WordPress Webサイトを構築する](https://intl.cloud.tencent.com/document/product/213/8044)
- [Discuz! フォーラムを構築する](https://intl.cloud.tencent.com/document/product/213/8043)


## 関連ドキュメント
- [インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)
- [SSHキーの管理](https://intl.cloud.tencent.com/document/product/213/16691)
