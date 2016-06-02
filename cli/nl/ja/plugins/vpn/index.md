---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# IBM VPN CLI
*最終更新日: 2016 年 5 月 3 日*

コマンド・ライン・インターフェース (CLI) を使用して、IBM® Virtual Private Network (VPN) サービスの構成と管理を実行できます。IBM VPN CLI は、Cloud Foundry CLI プラグインと共に使用するプラグインです。このプラグインは、Windows、MAC、Linux オペレーティング・システム用に使用可能です。環境に適したものを使用してください。

始めに、Cloud Foundry CLI をインストールします。詳しくは、「[Cloud Foundry command line interface](https://console.{DomainName}/docs/cli/downloads.html)」を参照してください。 

##IBM VPN CLI プラグインのインストール
**注:** 以前のバージョンの IBM VPN CLI プラグインがインストールされている場合は、まずそれをアンインストールする必要があります。次のコマンドを使用してください。 

```
cf uninstall-plugin vpn
```  

**ローカルでのインストール**

1. 使用するプラットフォームに対応した IBM VPN プラグインを「[IBM Bluemix CLI プラグイン・リポジトリー](http://plugins.ng.bluemix.net)」からダウンロードします。
2. 以下のコマンドを使用して、IBM VPN プラグインをインストールします。
**注:** VPN プラグインの場所に移動するか、またはプラグインの場所のパスを指定します。  

	**MS Windows OS の場合:**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**Apple MAC OS の場合:**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**Linux OS の場合:**

	```
	cf install-plugin vpn_linuxamd64
	```  


**Bluemix Repository からのインストール**  

1. Bluemix リポジトリーを Cloud Foundry CLI リポジトリーに追加します。次のコマンドを使用してください。

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. 次のコマンドを実行します。  

	```
	cf install-plugin vpn -r bluemix
	```
##IBM VPN サービスのコマンドのリスト

### cf vpn-create connection

VPN 接続を作成します。

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### パラメーター
{: #p1}

**connection name:**
接続の名前。

**gateway name:**
ゲートウェイの名前。

**-k:**
事前共有鍵。

**subnet/mask:**
CIDR フォーマットでのリモート・サブネット・アドレス。 

**customer gateway IP address:**
VPN トンネルのリモート・エンドポイント IP アドレス。 

##### オプション・パラメーター:
{: #op1}

**-d:** 指定されたパラメーターについての説明。

**-peer_id:** リモート・ピアの ID。VPN トンネルの他のエンドポイント。

**-admin_state:** VPN 接続の状況。値: UP または DOWN。

**-dpd-action:** ピアが非活動として検出された場合に実行するアクション。値: hold、clear、disabled、restart、restart-by-peer。デフォルト値: hold

**-gateway_ip:** ローカル VPN トンネル・エンドポイントの IP アドレス。 

**-i:** イニシエーターの状態。デフォルト値: bi-directional。

**-dpd-timeout:** セッションが終了するまでのタイムアウト値 (秒)。範囲: 6 秒以上 86400 秒以下。デフォルト値: 120 秒。キープアライブ・タイムアウトの値は、キープアライブ間隔の値よりも高くなければなりません。

**-dpd-interval:** キープアライブ間隔 (秒)。ピアの活動状態を検査するために、構成された間隔でキープアライブ・メッセージを送信します。範囲: 5 秒以上 86399 秒以下。デフォルト値: 15 秒

**-ike:** IKE ポリシーの名前。

**-ipsec:** IPSec ポリシーの名前。


### cf vpn-create ike

IKE ポリシーを作成します。

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### パラメーター
{: #p2}

**policy name:**
IKE ポリシーの名前。

**gateway name:**
ゲートウェイの名前。 

##### オプション・パラメーター:
{: #op2}

**-d:** 指定されたパラメーターについての説明。

**-pfs:** Diffie-Hellman (DH) グループ ID。値: Group2、Group5、Group14。デフォルト値: Group2 

**-e:** 暗号化アルゴリズム。値: aes-128、aes-192、aes-256、3des。デフォルト値: aes-128

**-lv:** IKE セキュリティー・アソシエーションの存続時間の値。範囲: 60 秒以上 86400 秒以下。デフォルト値: 86400 秒


### cf vpn-create ipsec

IPSec ポリシーを作成します。

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### パラメーター
{: #p3}

**policy name:**
IPSec ポリシーの名前。 

**gateway name:**
ゲートウェイの名前。 

##### オプション・パラメーター:
{: #op3}

**-d:** 指定されたパラメーターについての説明。

**-pfs:** Diffie-Hellman (DH) グループ ID。値: Group2、Group5、Group14。デフォルト値: Group2  

**-e:** 暗号化アルゴリズム。値: aes-128、aes-192、aes-256、3des。デフォルト値: aes-128

**-lv:** セキュリティー・アソシエーションの存続時間の値。範囲: 60 秒以上 86400 秒以下。デフォルト値: 3600 秒

### cf vpn-create gateway

VPN ゲートウェイを作成します。

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### パラメーター
{: #p4}

**gateway name:**
ゲートウェイの名前。

**-t:** サービスを有効にするコンテナー。値: allSingleContainers、allContainerGroups、allContainers。デフォルト値: デフォルト値はありません。いずれかのタイプを指定する必要があります。 

#####オプション・パラメーター:
{: #op4}

**-gateway_ip:**
ゲートウェイの IP アドレス。 

**-subnets:**
CIDR フォーマットでのサブネット・アドレス。 

### cf vpn-show gateways

現在のゲートウェイに関する情報を表示します。

```
cf vpn-show gateways
```
### cf vpn-show ikes

現在の IKE 接続に関する情報を表示します。

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

現在の IPSec 接続に関する情報を表示します。

```
cf vpn-show ipsecs
```
### cf vpn-show connections

すべての現行接続に関する情報を表示します。

```
cf vpn-show connections
```
### cf vpn-show ike

IKE 接続に関する情報を表示します。

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

IPSec 接続に関する情報を表示します。

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

ゲートウェイに関する接続情報を表示します。

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

特定の接続に関するすべての情報を表示します。

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

既存の接続、ポリシー、またはゲートウェイを削除します。

```
cf vpn-delete ike <policy name>
```

```
cf vpn-delete ipsec <policy name>
```

```
cf vpn-delete connection <connection name>
```

```
cf vpn-delete gateway <gateway name>
```


### cf vpn-update connection

既存の VPN 接続を更新します。

```
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### パラメーター
{: #p5}

**connection name:**
接続の名前。


##### オプション・パラメーター:
{: #op5}

**gateway name:**
ゲートウェイの名前。

**customer gateway IP address:**
VPN トンネルのリモート・エンドポイント IP アドレス。 

**subnet/mask:**
CIDR フォーマットでのサブネット・アドレス。 

**-k:**
事前共有鍵。

**-d:** 指定されたパラメーターについての説明。

**-peer_id:** リモート・ピアの ID。VPN トンネルの他のエンドポイント。

**-admin_state:** VPN 接続の状況。値: UP または DOWN。

**-dpd-action:** ピアが非活動として検出された場合に実行するアクション。値: hold、clear、disabled、restart、restart-by-peer。デフォルト値: hold

**-gateway_ip:** ローカル VPN トンネル・エンドポイントの IP アドレス。 

**-i:** イニシエーターの状態。デフォルト値: bi-directional。

**-dpd-timeout:** セッションが終了するまでのタイムアウト値 (秒)。範囲: 6 秒以上 86400 秒以下。デフォルト値: 120 秒

**-dpd-interval:** キープアライブ間隔 (秒)。ピアの活動状態を検査するために、構成された間隔でキープアライブ・メッセージを送信します。範囲: 5 秒以上 86399 秒以下。デフォルト値: 15 秒

**-ike:** IKE ポリシーの名前。

**-ipsec:** IPSec ポリシーの名前。


### cf vpn-update ike

IKE ポリシーを更新します。

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### パラメーター
{: #p6}

**policy name:**
IKE ポリシーの名前。 

##### オプション・パラメーター:
{: #op6}

**gateway name:** ゲートウェイの名前。 

**-d:** 指定されたパラメーターについての説明。

**-pfs:** Diffie-Hellman (DH) グループ ID。値: Group2、Group5、Group14。デフォルト値: Group2 

**-e:** 暗号化アルゴリズム。値: aes-128、aes-192、aes-256、3des。デフォルト値: aes-128

**-lv:** IKE セキュリティー・アソシエーションの存続時間の値。範囲: 60 秒以上 86400 秒以下。デフォルト値: 86400 秒


### cf vpn-update ipsec

IPSec ポリシーを更新します。

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### パラメーター
{: #p7}

**policy name:**
IPSec ポリシーの名前。


##### オプション・パラメーター:
{: #op7}

**gateway name:**
ゲートウェイの名前。

**-d:** 指定されたパラメーターについての説明。

**-pfs:** Diffie-Hellman (DH) グループ ID。値: Group2、Group5、Group14。デフォルト値: Group2 

**-e:** 暗号化アルゴリズム。値: aes-128、aes-192、aes-256、3des。デフォルト値: aes-128

**-lv:** セキュリティー・アソシエーションの存続時間の値。範囲: 60 秒以上 86400 秒以下。デフォルト値: 3600 秒

### cf vpn-update gateway

既存の VPN ゲートウェイを更新します。

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### パラメーター
{: #p8}

**gateway name:**
ゲートウェイの名前。

#####オプション・パラメーター:
{: #op8}

**-t:** サービスを有効にするコンテナー。値: allSingleContainers、allContainerGroups、allContainers。デフォルト値: デフォルト値はありません。いずれかのタイプを指定する必要があります。

**-gateway_ip:**
ゲートウェイの IP アドレス。 

**-subnets:**
CIDR フォーマットでのサブネット・アドレス。 

# 関連リンク
## 一般  
{: #general}  
* [IBM VPN service](../../../services/vpn/index.html)
* [Cloud Foundry CLI](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
