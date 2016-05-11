---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} について
{: #vpn_overview}  
*最終更新日: 2016 年 3 月 17 日*

{{site.data.keyword.vpn_full}} (VPN) サービスは、社内データ・センターと IBM Bluemix&reg; クラウド環境内リソースの間のセキュアな通信チャネルを提供します。この接続は、インターネットを介して確立されます。
{:shortdesc}

{{site.data.keyword.vpn_short}} サービスには、以下のフィーチャーがあります。  
##セキュリティー 
IBM VPN サービスは、業界標準の Internet Protocol Security (IPSec) プロトコル・スイートを使用して、社内データ・センターと IBM Bluemix クラウド環境の間で IP 通信の認証と暗号化を行います。IPSec は、ネットワーク・レベルのピア認証、データ保全性、およびデータ機密性 (暗号化) を提供します。

IBM VPN サービスは、以下の IPSec プロトコルと変換をサポートします。

* 認証アルゴリズム:
	* HMAC-SHA1-96。共有鍵の長さは 160 ビット (デフォルト)  
* 暗号化アルゴリズム:
	* 3DES-CBC。共有鍵の長さは 192 ビット
	* AES-CBC。共有鍵の長さは 128 (デフォルト)、192、256 ビット
* 認証と暗号化プロトコル:
	* 認証ヘッダー (AH) とカプセル化セキュリティー・ペイロード (ESP) のプロトコルがサポートされています。AH は認証のためだけに使用されます。ESP は認証と暗号化を提供するために使用されます。
* IKEv1 Diffie-Hellman (DH) Key Exchange グループ 2 (デフォルト)、5、14

IBM VPN サービスは、IPSec トンネル・モードをサポートします。このモードでは、IPSec が元の IP パケット全体を保護します。IPSec はパケットを暗号化し、それをカプセル化して新しい IP パケット内に入れ、その新しいパケットを IPSec ピアに転送します。 

IBM VPN サービスは Diffie-Hellman 鍵交換と事前共有鍵を使用して、2 つのピア間の関連付けを保護します。いずれかの側が事前共有鍵を提供しない場合、認証は失敗します。 
 
IBM VPN サービスは、以下の IETF RFC に準拠しています。

* IKEv1 用の RFC 2407、2408、2409
* IPv4 セキュリティー用の RFC 4301   
* IPv4 認証ヘッダー用の RFC 4302  
* IPv4 カプセル化セキュリティー・ペイロード (ESP) 用の RFC 4303  
* 認証用の RFC 2104 HMAC と RFC 2404 HMAC-SHA-1-96  
* 暗号化用の RFC 2451 3DES-CBC、RFC 3602 AES128-CBC、AES192-CBC、AES256-CBC
##容易さ
IBM VPN サービスは、シンプルで直観的なグラフィカル・インターフェースを使用して作成できます。ゲートウェイ IP アドレスとデータ・センターのサブネットを指定できます。デフォルトの IPSec と IKE ポリシーを使用するか、またはそれらのポリシーを必要に合わせてカスタマイズすることができます。  
##管理
IBM VPN サービスは、グラフィカル・インターフェース、[コマンド・ライン・インターフェース](../../cli/plugins/vpn/index.html)、または [API](https://new-console.ng.bluemix.net/apidocs/101) を使用して管理できます。

