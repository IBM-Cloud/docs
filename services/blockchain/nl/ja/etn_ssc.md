---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# IBM Secure Service Container
{: #etn_ssc}

最終更新日: 2016 年 10 月 13 日
{: .last-updated}

IBM Blockchain High Security Business Network は、ブロックチェーン・サービスをホストするための基本インフラストラクチャーを提供する IBM Secure Service Container へのアプライアンスとしてデプロイされます。このアプライアンスは、自律的に機能するオペレーティング・システム、Docker コンテナー、ミドルウェア、ソフトウェアの各コンポーネントを結合し、最適化されたセキュリティーが実装されたコア・サービスとインフラストラクチャーを提供します。
{:shortdesc}

IBM Secure Service Container は、機密性の高い規制対象のデータを扱うための Systems LinuxONE プラットフォームの高度な暗号化、セキュリティー、信頼性をブロックチェーン・サービスにもたらします。ブロックチェーンは、IBM Secure Service Container からの一連の機能によって保護されます。その機能として、カプセル化されたオペレーティング・システム、暗号化されたアプライアンス・ディスク、改ざん保護、保護されたメモリー、および強力な LPAR の隔離などがあり、EAL5+ の証明と一致するよう構成することができます。

以下のアーキテクチャーの図は、IBM Secure Service Container とブロックチェーン・アプライアンスの編成を示しています。

![アーキテクチャーの図](images/Architecture_HSBN_SSC.png "IBM Secure Service Container とブロックチェーン・アプライアンス")
*図 1. IBM Secure Service Container とブロックチェーン・アプライアンスの概要*
<br><br>
## 主なセキュリティー機能
IBM Secure Service Container は、ブロックチェーン・サービスに、以下の最適化されたセキュリティー機能を提供します。  

### システム管理者からの保護
>プラットフォーム管理者やシステム管理者であっても、アプライアンス・コードにアクセスすることはできません。データ・アクセスはアプライアンスによって制御されるため、無許可アクセスは不可能です。これは、処理中/保留中のすべてのデータの署名と暗号化の組み合わせによってサポートされます。メモリーへのアクセスもすべて除外されます。ファームウェアは、セキュア・ブート・アーキテクチャーによってこれをサポートします。

>ブロックチェーンが IBM Secure Service Container によって保護されている場合、システム管理者には、以下の制限があります。
>* ノードにアクセスできない
>* ブロックチェーン・ネットワークを表示できない

### 改ざんからの保護  
>IBM Secure Service Container は、LPAR メモリー・アクセスを提供するすべての外部インターフェースを無効にします。改ざんから保護したり別のものと交換したりできないようにするために、イメージ・ブート・ローダーは署名されています。

### 暗号化されたアプライアンス・ディスク
>ディスク上に保管されるコードとデータはすべて、Linux 暗号化レイヤーを使用して毎回暗号化されます。  
- カプセル化されたオペレーティング・システム
- 保護された IP
- 組み込みモニターと自己修復  
<br>

## REST API 経由でのアプライアンスの管理
ソフトウェア・アプライアンスは、信頼性があり、安全で、拡張が容易な z Systems プラットフォームで使用できるよう事前に構成されています。これらのアプライアンスは、構成なしで REST API によって管理できます。

REST API 経由でブロックチェーン資産を管理するために、Bluemix または REST コマンド・ツールで Blockchain ダッシュボードの Swagger UI を使用することができます (`curl` や `Postman` など)。

例えば、ネットワーク内のすべてのピアに関する情報を取得するには、`curl` を使用して以下のコマンドを発行します。
```
curl -u <username>:<password> https://<peer_ip>:<port>/network/peers
```
以下の curl のサンプル・コマンドと、それによって返される結果をご覧ください。
* コマンド:
```
curl -u dashboarduser_type0_2ef27***:89317***https://ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-api.blockchain.ibm.com:443/network/peers
```
* ネットワーク内のすべてのピアで返される情報:
```
{
	"peers": [{
		"ID": {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "rC0uvv0cbSbiT8RUGKPQM3q/o09oyWlcBmRxogi2Cls="
	},
	{
		"ID": {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "oeoI+Xa/lW8Xvrvv71A+Nvzit+JDa+oIkthpZHwfaTE="
	}]
}
```
REST API 経由でのブロックチェーンとの対話方法については、[ダッシュボード・モニター](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html)と[サンプルとチュートリアル](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html)を参照してください。
