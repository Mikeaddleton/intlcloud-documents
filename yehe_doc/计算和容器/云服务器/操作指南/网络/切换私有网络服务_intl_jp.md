## 概要

Tencent Cloudは、さまざまなシナリオに対応するために基幹ネットワークとVirtual Private Cloud（VPC）をご提供します。これに基づいて、我々はさらに柔軟なサービスを提供し、お客様がネットワークを管理するのに役立てます。
- ネットワーク間の切り替え
 - **基幹ネットワークからVPCへの切り替え**：Tencent Cloudは単一のCVMおよび複数のCVMの基幹ネットワークからVPCへの切り替えサービスをご提供いたします。
 - **VPC AからVPC Bへの切り替え**：Tencent Cloudは単一のCVMおよび複数のCVMのVPC AからVPC Bへの切り替えサービスをご提供いたします。
- カスタムIPの設定
- HostNameを保持することを選択します。

##  前提条件
移行前に、プライベート/パブリックネットワークのCLBおよびElastic Network Interface（ENI）のバインドを自身で解除し、プライマリENIの補助IPをリリースしてください。移行後に再びバインドします。


## 操作手順
### インスタンスのネットワーク属性の判断
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 「インスタンス」リストページで、実際に使用されているビューモードに従い、ネットワークを切り替えたいターゲットインスタンスを確認します。
<dx-tabs>
::: リストビュー
下図に示すように、「インスタンス設定」に表示されているネットワークが「基幹ネットワーク」であれば、そのインスタンスが所属するネットワークは基幹ネットワークです。
![](https://main.qcloudimg.com/raw/bb54a50bd8a42e5aeac6ce02bc3c6a4d.png)
:::
::: タブビュー
「基本情報」の中の「ネットワーク情報」に表示されているネットワークが「基幹ネットワーク」であれば、そのインスタンスが所属するネットワークは基幹ネットワークです。
:::
</dx-tabs>
<dx-alert infotype="notice" title="">
- 基幹ネットワークからVPCに切り替えた後は、元に戻せません。 CVMインスタンスは、基幹ネットワークからVPCに切り替えた後、他の基幹ネットワークのCVMインスタンスと通信できません。
基幹ネットワークからVPCに切り替える前に、移行したい基幹ネットワークCVMと同一リージョンのVPC、ならびに同一のアベイラビリティーゾーンのサブネットワークを事前に作成しておく必要があります。具体的には[VPCの作成](https://intl.cloud.tencent.com/document/product/215/31805)をご参照ください。
- インスタンスのネットワーク属性を把握した後は、必要に応じて[VPCへの切り替え](#changeVPC)手順を参照し、対応する操作を行ってください。
</dx-alert>





### VPCへの切り替え[](id:changeVPC)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 「インスタンス」ページで、ターゲットインスタンスをVPCに切り替えます。
<dx-tabs>
::: リストビュー

#### 単一インスタンスのVPCへの切り替え
下図に示すように、ネットワークを切り替えたいターゲットインスタンスを選択し、右側の操作バーで、**その他** > **リソース調整** > **VPCへの切り替え**を選択します。
	![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)


#### 複数インスタンスのVPCへの切り替え
下図に示すように、ターゲットインスタンスのVPCへの一括切り替えを行う必要がある場合は、ネットワークを切り替えたいインスタンスにチェックを入れ、インスタンスリストの上方で、**その他の操作** > **リソース調整** > **VPCへの切り替え**を選択します。
<dx-alert infotype="notice" title="">
CVMのネットワークタイプを一括で切り替える場合は、選択するCVMが必ず同一のアベイラビリティーゾーンになければなりません。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/b15f3e4e6c212ff496d38c3753c9a4da.png"/>
:::
::: タブビュー
下図に示すように、ネットワークを切り替えたいターゲットインスタンスのタブを選択し、右上隅の**その他の操作** > **リソース調整** > **VPCへの切り替え**を選択します。
![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)
:::
</dx-tabs>

3. ポップアップした「VPCへの切り替え」ウィンドウで、注意事項を確認し、**次のステップ**をクリックします。
4. VPCおよび対応するサブネットワークを選択し、**次のステップ**をクリックします。
![](https://main.qcloudimg.com/raw/acaca8c4343d8e5357bd33b75f1f5f68.png)
5. 実際のニーズに応じて、選択したサブネットワークで事前割り当てIPアドレスの設定を行い、HostNameオプションを設定し、**次のステップ**をクリックします。
<dx-alert infotype="explain" title="">
- 「事前割り当てIPアドレス」が未入力の場合、システムが自動的に割り当てます。
- HostNameオプションの設定の際、VPCへの切り替えと同時にインスタンスのHostNameをリセットするか、またはインスタンスの元のHostNameを維持するかを選択できます。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/c3908fef18c46a5f88aebfca2204f5c0.png"/>
6. 下図に示すように、シャットダウンプロンプトに従って操作を行い、**移行開始**をクリックし、コンソールページでインスタンスの変更ステータスを「インスタンスのvpc属性変更」とします。
<dx-alert infotype="notice" title="">
- 移行中、CVMインスタンスを再起動する必要があります。他の操作を行わないでください。
- 移行後、CVMインスタンスが正常に実行されており、プライベートネットワーク経由でアクセスでき、リモートログインできるかどうかを確認してください。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png"/>



