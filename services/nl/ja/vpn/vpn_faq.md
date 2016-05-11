---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} のよくある質問
{: #vpn_faq}
*最終更新日: 2016 年 3 月 17 日*

よくある質問を以下に示します。
{:shortdesc}

1. IBM VPN サービスとの相互運用性が IBM ラボによって検証されているサード・パーティー・ベンダー製のデバイスはどれですか?

	IBM ラボでは、以下の VPN ゲートウェイ・デバイスについて、IBM VPN サービスとの相互運用性をテストしました。

	* Cisco Adaptive Security Appliance (ASA) Software バージョン 8.2(1)。[構成例を参照してください](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7。[構成例を参照してください](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic。[構成例を参照してください](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic。[構成例を参照してください](vpn_onpremises.html#strongswan){: new_window}

	さらに、他のすべてのベンダーによる IPSec 規格に準拠した VPN ゲートウェイ・デバイスは、IBM VPN サービスと共に良好に機能すると考えられます。

2. ピアの障害はどれほど早く検出されますか?
 
	ピアの障害は、構成されたキープアライブ・タイムアウト値で検出されます。デフォルトの設定値は 60 秒です。

3. VPN サービスごとにいくつの VPN ゲートウェイや接続を作成できますか?
 
	Bluemix スペース内では VPN サービスごとに 1 つの VPN ゲートウェイ・アプライアンスを作成できます。VPN ゲートウェイごとに、さまざまな宛先に対する最大 16 の接続を定義できます。 

4. Bluemix Secure Gateway サービスではなく IBM VPN サービスを使用するのはどのような場合ですか?

	どちらのサービスを使用しても、Bluemix リソースとオンプレミス・データ・センターの間にセキュアな接続を提供できます。 

	IBM VPN サービスは、任意の 2 つのエンドポイント間に接続を確立するときに使用します。VPN サービスは、オンプレミス・ネットワークと IBM Bluemix クラウド環境の間に、セキュアなレイヤー 3 IPSec 接続を確立します。IBM VPN サービスは、IBM コンテナー (Docker コンテナー) のみにセキュアにアクセスするために使用できます。 

	Bluemix 内の特定のアプリケーション・エンドポイントからオンプレミス・データ・センター内の別のエンドポイントにセキュア接続を確立する場合は、Bluemix Secure Gateway サービスを使用します。 

5. IBM VPN サービスを使用することにより、IBM Bluemix クラウド環境内のコンテナーと仮想サーバーに、それぞれのプライベート IP アドレスを使用してアクセスできますか。
 
	現在、IBM VPN サービスは Bluemix コンテナーにアクセスするためにのみ使用可能です。

6. IBM VPN サービスを Bluemix 組織レベルで定義できますか?

	現在、IBM VPN サービスは Bluemix スペース・レベルでのみ使用可能です。Bluemix 組織に複数のスペースがある場合、各スペースに対して別個の VPN サービスを定義できます。

7. どのようにして IBM VPN サービスを SoftLayer Gateway Appliance サービス (GaaS) に接続できますか?

	IPSec トンネルを作成して、IBM VPN サービスと SoftLayer GaaS の間にセキュアな通信を確立できます。[構成例を参照してください。](vpn_onpremises.html#gaas){: new_window}
