---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} の開始
{: #vpn}  
*最終更新日: 2016 年 5 月 9 日*

{{site.data.keyword.vpn_full}} service for Bluemix&reg; は、IBM Bluemix クラウド環境内で IBM コンテナー (Docker コンテナー) にセキュアにアクセスするために使用できます。IBM Bluemix クラウド環境は、企業のデータ・センターの拡張として使用できます。また、IBM VPN サービスを使用して SoftLayer サーバーと接続することもできます。
{:shortdesc}

始める前に、IBM Docker コンテナーが使用可能であることを確認します。IBM Containers を作成して管理する方法について詳しくは、[IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html) を参照してください。  

最初に、Bluemix ダッシュボードで**仮想プライベート・ネットワーク**・サービス・インスタンス・タイルを選択します。以下の手順を実行します。

1. **「ゲートウェイの作成 (CREATE GATEWAY)」**を選択して {{site.data.keyword.vpn_short}} ゲートウェイを構成します。デフォルトのゲートウェイが作成されます。必要な場合、以下の手順に示されているようにゲートウェイ構成を編集します。
{: #gateway}  

  1. **「編集」**を選択します。  
  2. ゲートウェイ名を指定します。  
  3. VPN サービスを使用するコンテナーとコンテナー・グループを選択します。
**注:** コンテナーとコンテナー・グループのプライベート・サブネットは、VPN 接続によってアクセスできるように事前選択されています。
  4. **「保存」**を選択します。  

 デフォルトの IKE と IPSec ポリシーを使用することも、カスタム・ポリシーを構成することもできます。デフォルト・ポリシーを使用する場合は、ステップ 4 に進んでください。

2. **「IKE と IPSec ポリシー (IKE & IPSec Policies)」**タブを選択して、IKE ポリシーを構成します。
  1. **「新規追加 (ADD NEW)」**を選択します。  
  2. 以下の詳細を指定します。
	* **名前**: IKE ポリシーの名前
	* **許可アルゴリズム (Authorization Algorithm)**: sha1。これは変更できません  
	* **暗号化アルゴリズム**: ドロップダウンから選択します。値: aes-128 (デフォルト)、aes-192、aes-256、3des
	* **鍵ライフタイム (Key Lifetime)**: IKE セキュリティー・アソシエーションの存続時間の値 (秒)。範囲: 60 以上 86400 以下。デフォルト値: 86400
	* **PFS**: Diffie-Hellman (DH) グループ ID。値: Group2、Group5、Group14。デフォルト値: Group2
	* **ネゴシエーション・モード (Negotiation Mode)**: Main。これは変更できません
	* **バージョン**: IKEV1。これは変更できません
  3. **「保存」**を選択します。

3. 以下のようにして IPSec ポリシーを構成します。
  1. **「新規追加 (ADD NEW)」**を選択します。  
  2. 以下の詳細を指定します。
  	* **名前**: IPSec ポリシーの名前  
  	* **許可アルゴリズム (Authorization Algorithm)**: sha1。これは変更できません  
  	* **暗号化アルゴリズム**: ドロップダウンから選択します。値: aes-128 (デフォルト)、aes-192、aes-256、3des
  	* **鍵ライフタイム (Key Lifetime)**: セキュリティー・アソシエーションの存続時間の値 (秒)。範囲: 60 以上 86400 以下。デフォルト値: 3600
  	* **PFS**: Diffie-Hellman (DH) グループ ID。値: Group2、Group5、Group14。デフォルト値: Group2
  	* **変換プロトコル (Transform Protocol)**: ESP。これは変更できません
  	* **カプセル化モード (Encapsulation Mode)**: Tunnel。これは変更できません
  3. **「保存」**を選択します。  

4. データ・センターまたは SoftLayer サーバーの VPN ゲートウェイと IBM VPN ゲートウェイの間に接続を確立するための詳細を指定します。
{: #site}  

  1. **「ゲートウェイ・アプライアンス (Gateway Appliance)」**タブを選択します。
  2. **「サイト接続 (Site Connections)」**セクションで、**「接続の作成 (Create Connection)」**を選択します。
  3. 以下のサイト接続詳細を指定します。  
  	* **名前**: 接続の名前  
  	* **説明**: 接続についての説明 (オプション)  
  	* **事前共有鍵ストリング**: 認証に使用する事前共有 (秘密) 鍵
  	* **管理状態 (Admin State)**: VPN 接続の状況。ドロップダウンから選択します: UP または DOWN。デフォルト値: UP  
  	* **カスタマー・ゲートウェイ IP (Customer Gateway IP)**: VPN トンネルのリモート・エンドポイント IP アドレス  
  	* **カスタマー・サブネット (Customer Subnet)**: CIDR フォーマットでのリモート・サブネット・アドレス。別のサブネットを追加するには、正符号を選択します。
  4. (オプション) 以下の**「詳細設定」**パラメーターを構成します。  
  	* **IKE ポリシー (IKE Policy)**: IKE ポリシーを選択します。  
  	* **キープアライブ間隔 (Keep Alive Interval)**: キープアライブ間隔を秒数で指定します。ピアの活動状態を検査するために、構成された間隔でキープアライブ・メッセージを送信します。デフォルト値: 15。範囲: 5 以上 86399 以下
  	* **非活動のピアに対するアクション (Action on dead peer)**: ピアが非活動として検出された場合に実行するアクション。
    	値: 
  		* hold (デフォルト値): セキュリティー・アソシエーション (SA) は保持されます 
  		* clear: SA は削除されます
  		* disabled: SA は無効になります
  		* restart: SA は再ネゴシエーションされます
  		* restart-by-peer: 非活動のピアがあるすべての SA は再ネゴシエーションされます  
  	* **IPSec ポリシー (IPSec Policy)**: IPSec ポリシーを選択します。
  	* **キープアライブ・タイムアウト (Keep Alive Timeout)**: セッションが終了するまでのタイムアウト値 (秒)。デフォルト値: 120。範囲: 6 以上 86400 以下。キープアライブ・タイムアウトの値は、キープアライブ間隔の値よりも高くなければなりません。
  5. **「保存」**を選択します。

  **注:** 接続の確立中に、接続状況は ***作成の保留中* (*pending create*)** と表示されます。この状況が表示されたときには、接続のアクティブ状況が表示されるまで、画面を何回か最新表示してください。

**重要:** Web アプリケーションを使用している場合、その Web アプリケーションを、使用している Docker コンテナーにバインドする必要があります。このバインドは、トラフィックが IPSec VPN トンネルを通過するために必要です。

**重要:** IBM VPN サービスは、現在、レスポンダー・モードで作動しています。VPN 接続を開始するには、データ・パケットが IBM VPN ゲートウェイからオンプレミス・データ・センターまたは SoftLayer サーバーに向かって流れる必要があります。VPN 接続の確立後に、トラフィックは VPN 接続のエンドポイント間でどちらの方向にも流れることができます。

 
# 関連リンク
## サンプル 
{: #samples}  
* [オンプレミス strongSwan ゲートウェイ構成の例](vpn_onpremises.html#strongswan){: new_window}
* [オンプレミス Vyatta ゲートウェイ構成の例](vpn_onpremises.html#vyatta){: new_window}
* [オンプレミス SoftLayer Gateway Appliance Service (GaaS) 構成の例](vpn_onpremises.html#gaas){: new_window}
* [オンプレミス Cisco ASA 構成の例](vpn_onpremises.html#cisco){: new_window}

## API  
{: #api}  
* [IBM VPN RESTful API](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## 一般  
{: #general}  
* [IBM VPN コマンド・ライン・インターフェース](../../cli/plugins/vpn/index.html){: new_window}
* [IBM VPN FAQ](vpn_faq.html#vpn_faq){: new_window}
* [IBM Bluemix 料金シート](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix の前提条件](https://developer.ibm.com/bluemix/support/#prereqs)
