

接続するアクセラレーションドメイン名が次のような状況にある場合は、ドメイン名所有権を検証する必要があります。

- このドメイン名を初めて接続する
- このドメイン名が他のユーザーによって接続されている
- 接続するドメイン名が汎用ドメイン名である

## 操作手順

1.**検証方法**をクリックして、DNS検証に追加する必要がある解決レコード情報を取得します。検証が完了するまでページは開いたままにしてください。

2. ドメイン名解決サービスプロバイダがTencent Cloudの場合、[ドメイン名サービスコンソール](https://console.cloud.tencent.com/cns)でこのドメイン名を見つけて**解決**をクリックし、TXTのDNSレコードというレコードタイプを追加します。ホストレコードは`_cdnauth`と入力します。

3. TXT解決が有効になるのを待ち、**検証**ボタンをクリックして検証を行います。

