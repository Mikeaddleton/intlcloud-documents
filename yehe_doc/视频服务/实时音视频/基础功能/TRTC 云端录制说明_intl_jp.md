eラーニング、ステージライブストリーミング、ビデオミーティング、オンライン医療、リモートバンキングなどのユースケースでは、コンテンツ審査、録画アーカイブ、ビデオ再生などのニーズを考慮して、ビデオ通話やインタラクティブライブストリーミングのプロセス全体をレコーディングし保存する必要が度々出てきます。これらはクラウドレコーディング機能によって実現することができます。

## 機能の説明
TRTCのクラウドレコーディング機能では、REST APIインターフェースを呼び出してクラウドレコーディングタスクを開始し、レコーディングしたいオーディオビデオストリーミングをサブスクライブし、リアルタイムかつフレキシブルに管理することができます。また、開発者が自らサーバーやレコーディング関連モジュールをデプロイする必要がなく、より軽く使いやすくなっています。

- レコーディングモード：シングルストリーミングレコーディングでは、ルームの各ユーザーのオーディオビデオストリーミングをそれぞれ独立したファイルとしてレコーディングできます。ミクスストリーミングレコーディングでは、同一のルームのオーディオビデオメディアストリームを1つのファイルとしてレコーディングすることができます

* サブスクリプションストリーミング：サブスクリプションユーザーのブラックリスト/ホワイトリストを制定する方法で、サブスクライブしたいユーザーのメディアストリーミングを指定することができます
* トランスコードパラメータ：ミクスストリーミングのシーンで、コーデックのパラメータを設定することで、レコーディングするビデオファイルの品質を指定することができます
* ミクスストリーミングパラメータ：ミクスストリーミングのシーンで、複数のフレキシブルな自動マルチ画面レイアウトテンプレートやカスタムレイアウトテンプレートをサポートします
* ファイルストレージ：レコーディングしたファイルの保存先にクラウドストレージ/VODを指定することができます。現時点で、クラウドストレージベンダーはTencent CloudのCOSストレージをサポートし、VODベンダーはTencent Cloud VODをサポートしています
  （今後、その他のクラウドベンダーのストレージやVODサービスをサポートする場合があり、その際はお客様のクラウドサービスアカウントのご提供が必要です。クラウドストレージサービスにはストレージパラメータのご提供が必要です）
* コールバック通知：コールバック通知機能をサポートし、コールバックドメイン名を設定することで、クラウドレコーディングのイベントステータスがお客様のコールバックサーバーに通知されます

### シングルストリーミングレコーディング

![シングルストリーミングレコーディング](https://qcloudimg.tencent-cloud.cn/raw/cd843d26b27ed6f4179ebbff401ae6e3.png)

シングルストリーミングレコーディングのシーンを図にしたものです。ルーム1234でキャスター1とキャスター2がどちらもオーディオビデオストリーミングを行っています。キャスター1とキャスター2のオーディオビデオストリーミングをサブスクライブし、レコーディングモードをシングルストリーミングレコーディングに設定し、レコーディングバックエンドでキャスター1とキャスター2のオーディオビデオストリーミングをそれぞれプルし、それらを独立したメディアファイルとしてレコーディングすると仮定します。ファイルには次のものが含まれます。

1.  キャスター1のビデオM3U8インデックスファイル1個。
2.  キャスター1のいくつかのビデオTS分割ファイル。
3.  キャスター1のオーディオM3U8インデックスファイル1個。
4.  キャスター1のいくつかのオーディオTS分割ファイル。
5.  キャスター2のビデオM3U8インデックスファイル1個。
6.  キャスター2のいくつかのビデオTS分割ファイル。
7.  キャスター2のオーディオM3U8インデックスファイル1個。
8.  キャスター2のいくつかのオーディオTS分割ファイル。

レコーディングバックエンドはこれらのファイルを、お客様の指定するクラウドストレージサーバーにアップロードします。お客様の業務バックエンドはこれらのレコーディングファイルをプルし、業務ニーズに応じてファイルの結合やトランスコード操作を行う必要があります。[オーディオビデオの結合とトランスコードのスクリプト](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC)をご提供できます。

### ミクスストリーミングのレコーディング

![ミクスストリーミングレコーディング](https://qcloudimg.tencent-cloud.cn/raw/3a29f4527601abe3ac981759bf44ad07.png)

ミクスストリーミングレコーディングのシーンを図にしたものです。ルーム1234でキャスター1とキャスター2がどちらもオーディオビデオストリーミングを行っています。キャスター1とキャスター2のオーディオビデオストリーミングをサブスクライブし、レコーディングモードをミクスストリーミングレコーディングに設定し、レコーディングバックエンドでキャスター1とキャスター2のオーディオビデオストリーミングをそれぞれプルし、それらのビデオストリームを設定したマルチ画面テンプレートに従ってミクスストリーミングし、オーディオストリームをミキシングし、最後にメディアストリームを1つのメディアファイルに統合すると仮定します。ファイルには次のものが含まれます。

1.  ミクスストリーミング後のビデオM3U8インデックスファイル1個。
2.  ミクスストリーミング後のいくつかのビデオTS分割ファイル。

レコーディングバックエンドはこれらのファイルを、お客様の指定するクラウドストレージサーバーにアップロードします。お客様の業務バックエンドはこれらのレコーディングファイルをプルし、業務ニーズに応じてファイルの結合やトランスコード操作を行う必要があります。[オーディオビデオの結合とトランスコードのスクリプト](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC)をご提供できます。

> !
>- レコーディングインターフェースの呼び出し頻度は20qpsに制限されています
>- 1つのインターフェースのタイムアウト時間は6秒です
>- デフォルトでサポートされている同時レコーディングチャネル数は100チャネルです。チャネル数を増やしたい場合は、[チケットを提出](https://console.intl.cloud.tencent.com/workorder/category?step=0&source=14)してご連絡ください。
>- 1つのレコーディングタスクにつき、同時サブスクリプションをサポートする1ルーム内のオーディオビデオストリーミングは最大で25チャネルです。

## 呼び出しフロー
### 1. レコーディング開始

お客様のバックエンドサービスからREST API （CreateCloudRecording）を呼び出してクラウドレコーディングを開始します。特に重視すべきパラメータは次のとおりです。

#### タスクID（TaskId）

このパラメータはそのレコーディングタスクの固有識別子であり、後にこのレコーディングタスクインターフェースの操作を行うための入力パラメータとして、このタスクIDを保存しておく必要があります。

#### レコーディングモード（RecordMode）
- シングルストリーミングレコーディングでは、ルーム内でお客様がサブスクライブしたキャスターのオーディオおよびビデオファイルをそれぞれレコーディングし、レコーディングファイル（M3U8/TS）をクラウドストレージにアップロードします。
- ミクスストリーミングレコーディングでは、ルーム内でお客様がサブスクライブしたすべてのキャスターのオーディオビデオストリーミングを1つのオーディオビデオファイルにレコーディングし、レコーディングファイル[M3U8/TS]をクラウドストレージにアップロードします。

#### レコーディングユーザーのブラックリスト/ホワイトリスト（SubscribeStreamUserIds）
デフォルトでは、クラウドレコーディングはルーム内のすべてのメディアストリーム（最大25チャネル）をサブスクライブできます。このパラメータによって、サブスクライブするキャスターユーザーのブラックリスト/ホワイトリスト情報を指定することも可能です。もちろん、レコーディング中の更新操作もサポートしています。

#### クラウドストレージパラメータ（StorageParams）
クラウドストレージパラメータを指定すると、レコーディング後のファイルはお客様がアクティブ化した指定のクラウドストレージ/VODサービスにアップロードされます。クラウドストレージ/VODスペースのパラメータの有効性と、未払いの料金がない状態を維持するようご注意ください。ここでは、レコーディングファイルの名前に決まったルールがあることに注意が必要です

##### レコーディングファイル名の命名ルール

* シングルストリーミングレコーディングのM3U8ファイル名ルール：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* シングルストリーミングレコーディングのTSファイル名ルール：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* シングルストリーミングレコーディングのmp4ファイル名ルール：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Index>.mp4

* ミクスストリーミングレコーディングのM3U8ファイル名ルール：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>.m3u8

* ミクスストリーミングレコーディングのTSファイル名ルール：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

* ミクスストリーミングレコーディングのmp4ファイル名ルール：
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<Index>.mp4

* 高可用性プル後のファイル名ルール
クラウドレコーディングサービス中にデータセンターに障害が発生した場合、高可用性ソリューションによってレコーディングタスクを復旧させることがあります。このような場合、元のレコーディングファイルを上書きしないよう、プル後にプレフィックスha<1/2/3>を付けることで、高可用性の発生回数を表します。1つのレコーディングタスクにつき、プルの回数が最大で3回まで許容されます。

* シングルストリーミングレコーディングのM3U8ファイル名ルール：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* シングルストリーミングレコーディングのTSファイル名ルール：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* ミクスストリーミングレコーディングのM3U8ファイル名ルール：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>.m3u8

* ミクスストリーミングレコーディングのTSファイル名ルール：
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

#### フィールドの意味の説明：
\<Prefix>: レコーディングパラメータに設定するファイル名プレフィックスです。設定していなければ存在しません。
\<TaskId>: レコーディングのタスクIDです。世界唯一のもので、レコーディング開始後に返されるパラメータ内に付帯します。
\<SdkAppId>: レコーディングタスクのSdkAppIdです。
\<RoomId>: レコーディングルーム番号です。
\<UserId>: 特殊なbase64処理後のレコーディングストリームのユーザーIDです。下記の注意事項をご参照ください。
\<MediaId>: メイン/サブストリームを識別します。mainまたはauxです。
\<Type>: レコーディングストリームのタイプです。audioまたはvideoです。
\<UTC>: このファイルのUTCレコーディングの開始時間です。タイムゾーンはUTC+0で、年、月、日、時間、分、秒およびミリ秒から成ります。
\<Index>: mp4分割ロジック（サイズが2GBを超えるか、時間が24時間を超える）がトリガーされていなければ、このフィールドはありません。トリガーされている場合は分割ファイルのインデックス番号であり、1から順に付与されます。
ha\<1/2/3>：高可用性プルのプレフィックスです。例えば、最初のプルにより、\<Prefix>/\<TaskId>/ha1\_\<SdkAppId>\_\<RoomId>.m3u8に変わります。
>! ここで\<RoomId>が文字列のルームIDの場合、ルームIDに対してまずbase64操作を行ってから、base64後の文字列中の記号'/'を'-' (ダッシュ)に、記号'='を'.'にそれぞれ置き換えます。
レコーディングストリームの\<UserId>についてはまずbase64操作を行ってから、base64後の文字列中の記号'/'を'-' (ダッシュ)に、記号'='を'.'にそれぞれ置き換えます。

#### レコーディング開始時間の取得
レコーディング開始時間の定義は、最初にキャスターのオーディオビデオデータを受信し、最初のファイルのレコーディングを開始したサーバーunix時間です。
次の3つの方法で、レコーディング開始のタイムスタンプを取得することができます。

* レコーディングファイルインターフェース（DescribeCloudRecording）のBeginTimeStampフィールドを照会する

例えば、次の照会インターフェースから返された情報からは、BeginTimeStampは1622186279144msであることがわかります。

```json
{
  "Response":{
    "Status": "xx",
    "StorageFileList": [
      {
        "TrackType": "xx",
        "BeginTimeStamp": 1622186279144,
        "UserId": "xx",
        "FileName": "xx"
      }
    ],
    "RequestId": "xx",
    "TaskId": "xx"
  }
}
```

* M3U8ファイル中の、対応するタグの項目（\#EXT-X-TRTC-START-REC-TIME）を読みとる

例えば、次のM3U8ファイルからは、レコーディング開始時間のunixタイムスタンプが1622425551884msであることがわかります。

```m3u8
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-ALLOW-CACHE:NO
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-TARGETDURATION:70
#EXT-X-TRTC-START-REC-TIME:1622425551884
#EXT-X-TRTC-VIDEO-METADATA:WIDTH:1920 HEIGHT:1080
#EXTINF:12.074
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094551825.ts
#EXTINF:11.901
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094603825.ts
#EXTINF:12.076
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094615764.ts
#EXT-X-ENDLIST
```

* レコーディングコールバックイベントを監視する

サブスクリプションのコールバックにより、イベントタイプ307のBeginTimeStampフィールドで、レコーディングファイルに対応するレコーディング開始時間のタイムスタンプを取得することができます。
例えば、次のコールバックイベントからは、このファイルのレコーディング開始時間のunixタイムスタンプが1622186279144msであることが読み取れます。

```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

#### ミクスストリーミングレコーディングのウォーターマークパラメータ（MixWatermark）
ミクスストリーミングレコーディング中の、画像ウォーターマーク追加をサポートしています。最大サポート数は25個で、キャンバスの任意の位置にウォーターマークを追加することができます。

|フィールド名|説明|
|---|---|
|Top|ウォーターマークの左上隅に対しての垂直移動|
|Left|ウォーターマークの左上隅に対しての水平移動|
|Width|ウォーターマークの表示幅|
|Height|ウォーターマーク表示の高さ|
|url|ウォーターマークファイルの保存先url|

#### ミクスストリーミングレコーディングのレイアウトモードパラメータ（MixLayoutMode）
9グリッドレイアウト（デフォルト）、フロートレイアウト、画面共有レイアウト、カスタムレイアウトの、4種類のレイアウトをサポートしています

##### 9グリッドレイアウト：

キャスターの数に応じて各画面のサイズは自動調整されます。各キャスターの画面サイズは同一で、最大25画面をサポートします。

* サブ画面が1枚の場合：
各小画面の幅と高さはそれぞれキャンバス全体の幅と高さとなります。

* サブ画面が2枚の場合：
各小画面の幅はキャンバス全体の幅の1/2となります。
各小画面の高さはキャンバス全体の高さとなります。

* サブ画面が4枚以下の場合：
各小画面の幅と高さはそれぞれキャンバス全体の幅と高さの1/2となります。

* サブ画面が9枚以下の場合：
各小画面の幅と高さはそれぞれキャンバス全体の幅と高さの1/3となります。

* サブ画面が16枚以下の場合：
各小画面の幅と高さはそれぞれキャンバス全体の幅と高さの1/4となります。

* サブ画面が16枚を超える場合：
各小画面の幅と高さはそれぞれキャンバス全体の幅と高さの1/5となります。

 9グリッドレイアウトはサブスクリプションのサブ画面が増えるに従って、下図のように変化します。

![9グリッドレイアウト1](https://qcloudimg.tencent-cloud.cn/raw/9d989363167bd9231a1ebf3097b8fb5c.jpg)
![9グリッドレイアウト2](https://qcloudimg.tencent-cloud.cn/raw/cd5437606f3a5dceb723d6e63eb283ee.jpg)
![9グリッドレイアウト3](https://qcloudimg.tencent-cloud.cn/raw/98295756807b1aba1457f668f85d7fd9.jpeg)
![9グリッドレイアウト4](https://qcloudimg.tencent-cloud.cn/raw/87b3d8d21d3e22704c379a534faf37b8.jpeg)
![9グリッドレイアウト5](https://qcloudimg.tencent-cloud.cn/raw/3418887536457bfa607ecdfb34a71b7f.jpeg)
![9グリッドレイアウト6](https://qcloudimg.tencent-cloud.cn/raw/ae3aa97ee2cbe5678f1672b34a610d20.jpeg)

##### フロートレイアウト：
デフォルトでは最初に入室したキャスター（キャスター1名を指定することもできます）のビデオ画面はスクリーン全体となります。その他のキャスターのビデオ画面は左下隅から順に、入室の順序に従って水平に並び、小画面として表示され、小画面が大画面の上にフロート表示されます。画面の数が17枚以下の場合は、1列に4画面（4 x 4列）となります。画面の数が17枚より多い場合は、小画面が1列に5画面（5 x 5列）となるよう再レイアウトされます。最大25画面をサポートし、ユーザーがオーディオのみを送信している場合でも、画面の位置を占有することができます。

* サブ画面が17枚以下の場合：
       各小画面の幅と高さはそれぞれキャンバス全体の幅と高さ×0.235となります。
       隣接する小画面の左右と上下の間隔はそれぞれキャンバス全体の幅と高さ×0.012となります。
       小画面からキャンバスの縦枠および横枠までの余白も、それぞれキャンバス全体の幅と高さ×0.012となります。

* サブ画面が17枚を超える場合：
       各小画面の幅と高さはそれぞれキャンバス全体の幅と高さ×0.188となります。
       隣接する小画面の左右と上下の間隔はそれぞれキャンバス全体の幅と高さ×0.01となります。
       小画面からキャンバスの縦枠および横枠までの余白も、それぞれキャンバス全体の幅と高さ×0.01となります。

  フロートレイアウトはサブスクリプションのサブ画面が増えるに従って、下図のように変化します。
   ![フロートレイアウト1](https://qcloudimg.tencent-cloud.cn/raw/96a531ba9f6a69297ea4f1a5a365794a.jpg)
   ![フロートレイアウト2](https://qcloudimg.tencent-cloud.cn/raw/be91b17b6b557fcd7d1d76c589e15917.jpg)


##### 画面共有レイアウト：
キャスター1名を画面左側の大画面位置に指定し（指定しない場合、大画面位置は背景色になります）、その他のキャスターは右側に上から下へ順に垂直に配置します。画面の数が17枚より少ない場合は、右側の各列に最大8名、最大2列まで配置します。画面の数が17枚より多い場合は、17枚目以降のキャスターの画面を左下隅から順に水平に配置します。最大24画面をサポートし、キャスターがオーディオのみを送信している場合でも、画面の位置を占有することができます。

* サブ画面が5枚以下の場合:
右側の小画面の幅はキャンバス全体の幅の1/5、右側の小画面の高さはキャンバス全体の高さの1/4となります。
左側の大画面の幅はキャンバス全体の幅の4/5、左側の大画面の高さはキャンバス全体の高さとなります。

* サブ画面が5枚を超え、7枚以下の場合:
右側の小画面の幅はキャンバス全体の幅の1/7、右側の小画面の高さはキャンバス全体の高さの1/6となります。
左側の大画面の幅はキャンバス全体の幅の6/7、左側の大画面の高さはキャンバス全体の高さとなります。
* サブ画面が7枚を超え、9枚以下の場合:
右側の小画面の幅はキャンバス全体の幅の1/9、右側の小画面の高さはキャンバス全体の高さの1/8となります。
左側の大画面の幅はキャンバス全体の幅の8/9、左側の大画面の高さはキャンバス全体の高さとなります。

* サブ画面が9枚を超え、17枚以下の場合:
右側の小画面の幅はキャンバス全体の幅の1/10、右側の小画面の高さはキャンバス全体の高さの1/8となります。
左側の大画面の幅はキャンバス全体の幅の4/5、左側の大画面の高さはキャンバス全体の高さとなります。

* サブ画面が17枚を超える場合:
右（下）側の小画面の幅はキャンバス全体の幅の1/10、右（下）側の小画面の高さはキャンバス全体の高さの1/8となります。
左側の大画面の幅はキャンバス全体の幅の4/5、左側の大画面の高さはキャンバス全体の高さの7/8となります。

画面共有レイアウトはサブスクリプションのサブ画面が増えるに従って、下図のように変化します。
   ![画面共有レイアウト1](https://qcloudimg.tencent-cloud.cn/raw/d64e7e705060d21ec24d7392f8d43728.png)
   ![画面共有レイアウト2](https://qcloudimg.tencent-cloud.cn/raw/695683aecb62c29976f16124d6e9b29b.png)
   ![画面共有レイアウト3](https://qcloudimg.tencent-cloud.cn/raw/8423e777eb1a5bfb80e384e7b97db49d.png)
   ![画面共有レイアウト4](https://qcloudimg.tencent-cloud.cn/raw/538faeb7d2f993427b7ab1db548cb633.png)
   ![画面共有レイアウト4](https://qcloudimg.tencent-cloud.cn/raw/f911eb5a849da0aa22ed9b69ebe2f63a.png)

##### カスタムレイアウト：
業務の必要性に応じ、MixLayoutList内で各キャスター画面のレイアウト情報をカスタマイズできます。

### 2. レコーディング照会（DescribeCloudRecording）
必要に応じ、このインターフェースを呼び出してレコーディングサービスのステータスを照会することができます。レコーディングタスクが存在する場合にのみ、情報の照会が可能なことにご注意ください。レコーディングタスクがすでに終了している場合はエラーが返されます。
レコーディングしたファイルのリスト（StorageFile）には、今回レコーディングしたすべてのM3U8インデックスファイルおよびレコーディング開始時のUnixタイムスタンプ情報が含まれます。VODにアップロードしたタスクについては、このインターフェースから返されるStorageFileは空となることにご注意ください。

### 3. レコーディング更新（ModifyCloudRecording）
必要に応じ、このインターフェースを呼び出してレコーディングサービスのパラメータを変更することができます。例えば、サブスクリプションのブラックリスト/ホワイトリストSubscribeStreamUserIds（シングルストリーミングとミクスストリーミングレコーディングで有効）、レコーディングテンプレートのパラメータMixLayoutParams（ミクスストリーミングレコーディングで有効）などがあります。更新操作はすべて上書きの操作であり、増分更新の操作ではないことにご注意ください。毎回の更新時に、テンプレートパラメータMixLayoutParamsおよびブラックリスト/ホワイトリストSubscribeStreamUserIdsを含む、全情報を引き継ぐ必要があるため、以前のレコーディング開始パラメータまたは再計算した完全なレコーディング関連パラメータを保存する必要があります。

### 4. レコーディング停止（DeleteCloudRecording）
レコーディング終了後に、レコーディング停止（DeleteCloudRecording）インターフェースを呼び出してレコーディングタスクを終了する必要があります。これを行わなかった場合、レコーディングタスクは設定したタイムアウト時間MaxIdleTimeになると自動的に終了します。注意が必要な点は、MaxIdleTimeの定義が、ルーム内に継続的にキャスターがいない状態がMaxIdleTimeの時間を超えることを指す点です。ルーム内にキャスターが存在しているが、キャスターがデータをアップストリームしていないという場合は、タイムアウト時間のカウント状態に入りません。レコーディング終了時にこのインターフェースを呼び出してレコーディングタスクを終了することをお勧めします。

## 高度な機能

### mp4ファイルのレコーディング

レコーディングの出力ファイル形式をmp4形式にしたい場合は、レコーディング開始パラメータ(OutputFormat)でレコーディングファイルの出力形式をhls+mp4に指定することができます。デフォルトではhlsファイルへのレコーディングのままですが、hlsレコーディングの終了後、ただちにmp4への変換タスクがトリガーされ、hlsの存在するcos内からプルされてmp4パッケージ化が行われ、お客様のcosにアップロードされます。
ここではCOSのファイルプル権限を提供する必要があることにご注意ください。これを行わなければ、mp4変換タスクはhlsファイルのプル失敗によって中止されます。
mp4ファイルは次のような場合、強制的に分割されます。

1. レコーディングファイルの長さが24時間を超えた場合。
2. 1個のmp4ファイルのサイズが2GBに達した場合。
   <br>具体的なフローは図のとおりです
   <br>![mp4への出力](https://qcloudimg.tencent-cloud.cn/raw/d3a3f5121e9832cc8a39b8d9ec6f7b1a.png)

### レコーディングのVODへのアップロード

レコーディングした出力ファイルをVODプラットフォームにアップロードしたい場合は、レコーディング開始のストレージパラメータ(StorageParams)の中でCloudVodメンバーパラメータを指定することができます。レコーディングバックエンドはレコーディング終了後、レコーディングしたmp4ファイルを指定された方式でVODプラットフォームにアップロードし、コールバックの形式で再生アドレスをお客様に送信します。レコーディングモードがシングルストリーミングレコーディングモードの場合は、各サブスクリプションのキャスターが1つずつ対応する再生アドレスを持っています。レコーディングモードがミクスストリーミングレコーディングモードの場合は、ミクスストリーミング後のメディアの再生アドレスは1つのみとなります。VODアップロードタスクには次のいくつかの注意事項があります。

1. ストレージパラメータ中のCloudVodとCloudStorageは同時に1つしか指定できません。それ以上を指定した場合はレコーディングの開始に失敗します。
2. VODアップロードタスクの過程でDescribeCloudRecordingを使用して照会したタスクステータスには、レコーディングファイルの情報が含まれません。
   <br>具体的なフローは図のとおりです。ここに記載したクラウドストレージはレコーディング内部のクラウドストレージであり、お客様が関連のパラメータを入力する必要はありません。
   <br>![vodへの出力](https://qcloudimg.tencent-cloud.cn/raw/28da00ba87fc1b9be2030f96d2dfd820.png)



### シングルストリーミングファイル結合スクリプト

[シングルストリーミングオーディオビデオファイル結合スクリプト]()をご提供しています。シングルストリーミングレコーディングのオーディオビデオファイルを結合してMP4ファイルとするために用います。

>? 2つの分割ファイル間の時間間隔が15秒を超え、その間に何のオーディオ/ビデオ情報もない場合（サブストリームを無効にしている場合、サブストリーム情報は無視できます）、2つの分割ファイルはそれぞれ異なるセグメントであると判断されます。それらのうちレコーディング時間が早い方の分割ファイルが前のセグメントの終了分割ファイル、レコーディング時間が遅い方の分割ファイルが後のセグメントの開始分割ファイルとそれぞれ判断されます。

 - セグメントモード（-m 0）
このモードでは、スクリプトは各UserId下のレコーディングファイルをセグメントごとに結合し、1つのUserId下のセグメントがそれぞれのファイルに独立して結合されます。
 - 結合モード（-m 1）
同一のUserId下の全セグメントを1つのオーディオビデオファイルとして結合します。-sオプションを利用して、各セグメント間の間隔を埋めるかどうかを選択できます。

#### 依存環境

Python3

-   Centos: sudo yum install python3
-   Ubuntu: sudo apt-get install python3

Python3依存パッケージ

-	sortedcontainers：pip3 install sortedcontainers

#### 使用方法

 1.結合スクリプトを実行します：python3 TRTC_Merge.py [option]
 2.レコーディングファイルディレクトリ下で結合後のmp4ファイルを生成します
例：python3 TRTC_Merge.py -f /xxx/file -m 0

オプションパラメータおよび対応する機能は下表のとおりです。

|パラメータ| 機能 |
|---|---|
|-f | 結合対象のファイルのストレージパスを指定します。複数のUserIdを持つレコーディングファイルの場合、スクリプトはそれぞれ結合操作を行います。 |
|-m   | 0：セグメントモード(デフォルト設定)。このモードでは、スクリプトは各UserId下のレコーディングファイルをセグメントごとに結合します。各UserIdにつき、複数のファイルが生成される可能性があります。<br>1：結合モード。1つのUserId下の全オーディオビデオファイルを1つのファイルとして結合します。|
|-s|保存モード。このパラメータを設定すると、結合モードにおけるセグメント間の空白部分が削除されます。ファイルの実際の時間は物理時間より短くなります。|
|-a|0: メインストリーム結合(デフォルト設定)。同一のUserIdのメインストリームをオーディオと結合させます。サブストリームはオーディオと結合しません。 <br>1: 自動結合。メインストリームが存在する場合は、メインストリームをオーディオと結合し、メインストリームが存在せずサブストリームが存在する場合は、サブストリームをオーディオと結合します。 <br>2: サブストリーム結合。同一のUserIdのサブストリームをオーディオと結合させます。メインストリームはオーディオと結合しません|
|-p|出力するビデオのfpsを指定します。デフォルトでは15fps、有効範囲は5～120fpsです。5fps未満は5fpsとして、120fpsを超える場合は120fpsとしてカウントします。|
|-r|出力するビデオの解像度を指定します。-r 640 360であれば、出力するビデオの幅が640、高さが360であることを表します。|

**ファイル名のルール**

- オーディオビデオファイル名のルール：UserId\_timestamp\_av.mp4
- オーディオのみのファイル名のルール：UserId\_timestamp.m4a

>? ここでのUserIdはレコーディングストリームのユーザーIDの特殊なbase64値です。詳細についてはレコーディング開始の項のファイル名命名ルールに関する説明をご参照ください。timestampは各セグメントの最初のts分割ファイルのレコーディング開始時間となっています。



## コールバックインターフェース

コールバックを受信するHttp/Httpsサービスゲートウェイを設けてコールバックメッセージをサブスクライブすることができます。関連するイベントが発生した際、クラウドレコーディングシステムによってイベント通知がお客様のメッセージ受信サーバーにコールバックされます。

### イベントコールバックメッセージ形式

イベントコールバックメッセージは、HTTP/HTTPS POSTリクエストとしてサーバーに送信されます。以下がその詳細となります。
文字エンコード形式：UTF-8。
リクエスト：bodyの形式はJSONです。
応答：HTTP STATUS CODE = 200、サーバーは応答パケットの具体的な内容を無視します。プロトコルとの親和性のため、クライアントの応答内容に、JSON：`{"code":0}`を付けることをお勧めします。

### パラメータの説明

イベントコールバックメッセージのheaderには、次のフィールドが含まれています。


| フィールド名       | 値                 |
| ------------ | ------------------ |
| Content-Type | application/json   |
| Sign         | 署名値             |
| SdkAppId     | sdk application id |

イベントコールバックメッセージのbodyには、次のフィールドが含まれています。

| フィールド名       | タイプ        | 意味                                                         |
| ------------ | ----------- | ------------------------------------------------------------ |
| EventGroupId | Number      | イベントグループID。クラウドレコーディングでは3に固定されています                                  |
| EventType    | Number      | コールバック通知のイベントタイプ                                           |
| CallbackTs   | Number      | イベントコールバックサーバーからお客様のサーバーに送信されるコールバックリクエストのUnixタイムスタンプ。単位はミリ秒 |
| EventInfo    | JSON Object | イベント情報                                                     |

イベントタイプの説明

| フィールド名                                                | タイプ | 意味                                                    |
| ----------------------------------------------------- | ---- | ------------------------------------------------------- |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START        | 301  | クラウドレコーディング レコーディングモジュール起動                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP         | 302  | クラウドレコーディング レコーディングモジュール退出                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START          | 303  | クラウドレコーディング アップロードモジュール起動                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO             | 304  | クラウドレコーディング m3u8インデックスファイルを生成し、初回生成とアップロードの成功後にコールバック |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP           | 305  | クラウドレコーディング アップロード終了                                       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER               | 306  | クラウドレコーディング マイグレーションが発生し、元のレコーディングタスクが新たなロードに移行した際にトリガー |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE            | 307  | クラウドレコーディング M3U8ファイル(最初のts分割ファイルの切り出し) 生成後にコールバック      |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR          | 308  | クラウドレコーディング アップロードモジュールにエラー発生                               |
| EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR | 309  | クラウドレコーディング デコード画像ファイルのダウンロード時にエラー発生                       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP              | 310  | クラウドレコーディング mp4レコーディングタスク終了、コールバックにはレコーディングしたmp4ファイル名を含める       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT            | 311  | クラウドレコーディング vodレコーディングタスクメディアリソースアップロード完了                    |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP              | 312  | クラウドレコーディング vodレコーディングタスク終了                                |


イベント情報の説明

| フィールド名  | タイプ          | 意味                                 |
| ------- | ------------- | ------------------------------------ |
| RoomId  | String/Number | ルーム名（タイプはクライアントのルーム番号タイプと同様） |
| EventTs | Number        | 時間で発生するUnixタイムスタンプ。単位は秒    |
| UserId  | String        | レコーディングボットのユーザーID                  |
| TaskId  | String        | レコーディングID。1回のクラウドレコーディングタスクの固有ID     |
| Payload | JsonObject    | イベントタイプごとに異なる定義             |

イベントタイプ301 EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START時のPayloadの定義

| フィールド名 | タイプ   | 意味                                               |
| ------ | ------ | -------------------------------------------------- |
| Status | Number | 0：レコーディングモジュール起動成功。1：レコーディングモジュール起動失敗。 |

```json
{
        "EventGroupId": 3,
        "EventType":    301,
        "CallbackTs":   1622186275913,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186275",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

イベントタイプ302 EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP時のPayloadの定義

| フィールド名    | タイプ   | 意味                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| LeaveCode | Number | 0：レコーディングモジュールが正常に呼び出し、レコーディングを停止して退出した。<br>1: レコーディングボットがクライアントから強制退室させられた。<br>2：クライアントがルームを解散した。<br>3：サーバーがレコーディングボットを強制退室させた。<br>4：サーバーがルームを解散した。<br>99：ルーム内にレコーディングボット以外のユーザーストリームがなく、指定の時間を超過したため退出した。<br>100：ルームのタイムアウトにより退出した。<br>101：同一のユーザーが同じルームに重複して入室したため、ボットを退出させた |

```json
{
        "EventGroupId": 3,
        "EventType":    302,
        "CallbackTs":   1622186354806,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186354",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "LeaveCode":    0
                }
        }
}
```

イベントタイプ303 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START時のPayloadの定義

| フィールド名 | タイプ   | 意味                                                   |
| ------ | ------ | ------------------------------------------------------ |
| Status | Number | 0：アップロードモジュールが正常に起動<br>1：アップロードモジュール初期化失敗。 |

```json
{
        "EventGroupId": 3,
        "EventType":    303,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

イベントタイプ304 EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO時のPayloadの定義

| フィールド名   | タイプ   | 意味             |
| -------- | ------ | ---------------- |
| FileList | String | 生成したM3U8ファイル名 |

```json
{
        "EventGroupId": 3,
        "EventType":    304,
        "CallbackTs":   1622191965350,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileList":     "xx.m3u8"
                }
        }
}
```


イベントタイプ305 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP時のPayloadの定義

| フィールド     | タイプ   | 意味                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | 0: 今回のレコーディングアップロードタスクは完了し、指定されたサードパーティクラウドストレージに全ファイルがアップロードされた<br>1：今回のレコーディングアップロードタスクは完了しているが、少なくとも1つ以上のファイルがサーバーまたはバックアップストレージ上で滞留している<br>2: サーバーまたはバックアップストレージ上で滞留していたファイルが復元され、指定されたサードパーティクラウドストレージにアップロードされた |

```json
{
        "EventGroupId": 3,
        "EventType":    305,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

イベントタイプ306 EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER時のPayloadの定義

| フィールド名 | タイプ   | 意味                    |
| ------ | ------ | ----------------------- |
| Status | Number | 0：今回のマイグレーションはすでに完了 |

```json
{
        "EventGroupId": 3,
        "EventType":    306,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

イベントタイプ307 EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE時のPayloadの定義

| フィールド名         | タイプ   | 意味                                |
| -------------- | ------ | ----------------------------------- |
| FileName       | String | m3u8ファイル名                          |
| UserId         | String | このレコーディングファイルに対応するユーザーID              |
| TrackType      | String | audio/video/audio_video             |
| BeginTimeStamp | Number | レコーディング開始時のサーバーUnixタイムスタンプ（ミリ秒) |


```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

イベントタイプ308 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR時のPayloadの定義

| フィールド名  | タイプ   | 意味                       |
| ------- | ------ | -------------------------- |
| Code    | String | サードパーティクラウドストレージから返されるcode     |
| Message | String | サードパーティクラウドストレージから返されるメッセージの内容 |


```json
{
  "Code": "InvalidParameter",
  "Message": "AccessKey invalid"
}

{
        "EventGroupId": 3,
        "EventType":    308,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Code":       "xx",
                        "Message":    "xx"
                }
        }
}
```

イベントタイプ309 EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR時のPayloadの定義

| フィールド名 | タイプ   | 意味          |
| ------ | ------ | ------------- |
| Url    | String | ダウンロードに失敗したurl |


```json
{
        "EventGroupId": 3,
        "EventType":    309,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Url":       "http://xx",
                }
        }
}
```

イベントタイプ310 EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP時のPayloadの定義

| フィールド名   | タイプ   | 意味                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| Status   | Number | 0: 今回のmp4レコーディングタスクは正常に終了し、指定されたサードパーティクラウドストレージに全ファイルがアップロードされた<br>1：今回のmp4レコーディングタスクは正常に終了しているが、少なくとも1つ以上のファイルがサーバーまたはバックアップストレージ上で滞留している<br>2: 今回のmp4レコーディングタスクは正常に終了しなかった(cosのhlsファイルのプルに失敗したことが原因の可能性あり) |
| FileList | String | 生成したM3U8ファイル名                                             |


```json
{
        "EventGroupId": 3,
        "EventType":    310,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "FileList": ["xxxx1.mp4", "xxxx2.mp4"]
                }
        }
}
```

イベントタイプ311 EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT時のPayloadの定義

| フィールド名    | タイプ   | 意味                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| Status    | Number | 0: このレコーディングファイルはVODプラットフォームに正常にアップロードされた<br>1：このレコーディングファイルがサーバーまたはバックアップストレージ上で滞留している<br>2: このレコーディングファイルのVODアップロードタスクに異常が発生した |
| UserId    | String | このレコーディングファイルに対応するユーザーID（レコーディングモードがミクスストリーミングモードの場合、このフィールドは空） |
| TrackType | String | audio/video/audio_video                                      |
| MediaId   | String | main/aux                                                     |
| FileId    | String | このレコーディングファイルのVODプラットフォームでの固有id                                 |
| VideoUrl  | String | このレコーディングファイルのVODプラットフォームでの再生アドレス                               |
| CacheFile | String | このレコーディングファイルに対応するmp4ファイル名（VODアップロード前）                  |
| Errmsg    | String | statueが0ではない場合、対応するエラー情報                                |


アップロード成功のコールバック：

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "TencentVod":   {
                            "UserId":       "xx",
                            "TrackType":    "audio_video",
                            "MediaId":      "main",
                            "FileId":       "xxxx",
                            "VideoUrl":     "http://xxxx"
                        }
                }
        }
}
```

アップロード失敗のコールバック：

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       1,
                        "Errmsg":       "xxx",
                        "TencentVod":   {
                            "UserId":       "123",
                            "TrackType":    "audio_video",
                            "CacheFile":    "xxx.mp4"
                        }
                }
        }
}
```

イベントタイプ312 EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP時のPayloadの定義

| フィールド     | タイプ   | 意味                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | 0: 今回のvodアップロードタスクは正常に終了した<br>1：今回のvodアップロードタスクは正常に終了しなかった |


```json
{
        "EventGroupId": 3,
        "EventType":    312,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```



## ベストプラクティス

レコーディングの高可用性を保証するため、Restful APIを統合する際は、次のいくつかの点に注意するようお勧めします。

1. CreateCloudRecordingリクエストを呼び出した後は、http responseに注目してください。リクエストが失敗した場合は、具体的なステータスコードに応じて必要なリトライポリシーをとる必要があります。

   エラーコードは「1次エラーコード」と「2次エラーコード」の組み合わせから成り、「InvalidParameter.SdkAppId」のようになっています。

   - 返されたCodeがInValidParameter.xxxxxであれば、入力したパラメータに誤りがあることを示しています。表示に従ってパラメータをチェックしてください。
   - 返されたCodeがInternalError.xxxxxであれば、サーバーエラーに遭遇したことを示しています。リターンが正常となり、taskidが得られるまで、同じパラメータを使用して何度かリトライすることができます。例えば、1回目は3sのリトライ、2回目は6sのリトライ、3回目は12sのリトライというように、バックオフを使用してポリシーをリトライすることをお勧めします。
   - 返されたCodeがFailedOperation.RestrictedConcurrencyであれば、お客様の同時レコーディングタスク数がバックエンドの予備リソースを超過したことを示しています(デフォルトでは100チャネル)。Tencent Cloudテクニカルサポートにご連絡いただき、最大同時チャネル数制限の調整を依頼してください。

2. CreateCloudRecordingを呼び出す際、指定するUserId/UserSigはレコーディングを行う単独のボットユーザーがルームに入室する際のidですので、TRTCルーム内のその他のユーザーと重複しないようにしてください。また、TRTCクライアントが入室するルームのタイプはレコーディングインターフェースが指定するルームのタイプと常に同じものにする必要があります。例えば、SDKがルームを新規作成する際に文字列のルームナンバーを使用した場合は、クラウドレコーディングのルームタイプもそれに合わせて文字列のルームナンバーに設定する必要があります。

3. レコーディングステータスの照会を行う場合、次のいくつかの方法でレコーディングに対応するファイル情報を取得することができます。

   - CreateCloudRecordingタスクの開始に成功してから約15秒後に、DescribeCloudRecordingインターフェースを呼び出してレコーディングファイルに対応する情報を照会します。ステータスがidleであることがわかった場合、レコーディングがアップストリームされたオーディオビデオストリームをプルできていなかったことを示しています。ルーム内にアップストリーム中のキャスターがいるかどうかを確認してください。
   - CreateCloudRecordingの開始に成功した後、ルーム内にオーディオビデオのアップストリームが存在することが確実な状況では、レコーディングファイル名の生成ルールに従ってレコーディングファイル名をスプライシングすることができます。具体的なファイル名ルールについては上記をご参照ください(ここにファイル名ルールへのリンクを貼る)。
   - レコーディングファイルのステータスはコールバックによってお客様のサーバーに送信されます。関連するコールバックをサブスクライブすると、レコーディングファイルのステータス情報を受け取ることができます。（ここにコールバックページへのリンクを貼る）
   - Cosを通じてレコーディングファイルを照会します。クラウドレコーディングの開始時点でcosに保存されているディレクトリを指定し、レコーディングタスクの終了後に、対応するディレクトリからレコーディングファイルを見つけることができます。

