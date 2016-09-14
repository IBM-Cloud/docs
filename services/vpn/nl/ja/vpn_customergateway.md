---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# データ・センターまたは SoftLayer サーバーでのゲートウェイの構成
{: #vpn_yourdatacenter}
*最終更新日: 2016 年 3 月 17 日*

{{site.data.keyword.vpn_short}} サービスとのセキュア接続を確立するには、データ・センターまたは SoftLayer サーバーに IPSec VPN ゲートウェイが必要です。データ・センターまたは SoftLayer サーバーで、以下の VPN ゲートウェイ構成が必要になります。

* VPN ゲートウェイがネットワーク・アドレス変換 (NAT) の背後にある場合にのみ、VPN ゲートウェイで NAT トラバーサルを有効にします。 
* IBM VPN サービスを構成する際に使用したものと同じ事前共有鍵を使用します。
* 以下のサブネットをリモート・サブネットとして追加します。
	* IBM Bluemix スペース内に単一コンテナーを作成した場合、172.31.0.0/16 を追加します。
	* IBM Bluemix スペース内にコンテナー・グループを作成した場合、172.30.0.0/16 を追加します。
	* IBM Bluemix スペース内に単一コンテナーとコンテナー・グループを作成した場合、172.31.0.0/16 と 172.30.0.0/16 を追加します。
* 暗号化、認証、そして PFS グループ設定が、IBM VPN ゲートウェイと VPN ゲートウェイとで同じであることを確認してください。
