---



copyright:

  years: 2015，2017

lastupdated: "2016-06-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 用の {{site.data.keyword.vpn_short}} プラグイン

*バージョン:* 1.4.0

コマンド・ライン・インターフェース (CLI) を使用して、{{site.data.keyword.vpn_full}} サービスの構成と管理を行うことができます。 {{site.data.keyword.vpn_short}} CLI プラグインには、2 つのバージョンがあります。1 つは Cloud Foundry CLI プラグインで使用するためのものであり、もう 1 つは {{site.data.keyword.Bluemix}} CLI プラグインで使用するためのものです。どちらのバージョンのプラグインも同じ機能を提供します。
{:shortdesc}

{{site.data.keyword.vpn_short}} プラグインには、Windows、MAC、および Linux オペレーティング・システム用があります。環境に適したものを使用してください。

以下の手順は、{{site.data.keyword.Bluemix_notm}} CLI プラグインで使用する場合の説明です。Cloud Foundry (cf) CLI プラグインでプラグインを使用する場合は、『[{{site.data.keyword.vpn_short}} CLI plug-in for cf CLI](../vpn/index.html)』を参照してください。


以下の説明では、Bluemix CLI 用 {{site.data.keyword.vpn_short}} プラグインでサポートされるすべてのコマンドをリストし、それぞれの名前、オプション、使用法、前提条件、説明、および例を示します。VPN プラグインのインストール方法については、『[Extend your Bluemix command line interface](../../index.html#cli_bluemix_ext)』を参照してください。

**注:** *前提条件*には、コマンドを使用する前に必要なアクションがリストされています。前提条件には、以下のアクションの 1 つ以上が含まれる場合があります。
<dl>
<dt>**エンドポイント**</dt>
<dd>このコマンドを使用する前に、`bluemix api` を介して API エンドポイントを設定する必要があります。</dd>
<dt>**ログイン**</dt>
<dd>このコマンドを使用する前に、`bluemix login` コマンドを使用してログインする必要があります。</dd>
<dt>**ターゲット**</dt>
<dd>このコマンドを使用する前に、`bluemix target` コマンドを使用して組織およびスペースを設定する必要があります。</dd>
</dl>


## bluemix vpn connection-create
VPN 接続を作成します。

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CONNECTION_NAME* (必須): 接続の名前。

-g *GATEWAY_NAME* (必須): ゲートウェイの名前。

-k *PRESHARED_KEY* (必須): 事前共有鍵。

-subnets "*SUBNET*/*MASK*" (必須): CIDR 形式のリモート・サブネット・アドレス。

-cip *CUSTOMER_GATEWAY_IP_ADDRESS* (必須): VPN トンネルのリモート・エンドポイント IP アドレス。

-d *DESCRIPTION* (オプション): 指定されたパラメーターの説明。

-peer_id *PEER_ID* (オプション): リモート・ピアの ID。VPN トンネルの相手側のエンドポイント。

-admin_state *ADMIN_STATE* (オプション): VPN 接続の状況。有効な値は、`UP` または `DOWN` です。

-dpd-action *ACTION* (オプション): ピアが非活動として検出された場合に取るアクション。有効な値は、`hold`、`clear`、`disabled`、`restart`、または `restart-by-peer` です。デフォルト値は `hold` です。

-gateway_ip *IP_ADDRESS* (オプション): ローカル VPN トンネル・エンドポイントの IP アドレス。

-i *INITIATOR_STATE* (オプション): イニシエーターの状態。デフォルト値は `bi-directional` です。

-dpd-timeout *VALUE* (オプション): セッションが終了するまでのタイムアウト値 (秒)。範囲: 6 秒から 86400 秒。デフォルト値は `120` 秒です。

-dpd-interval *VALUE* (オプション): キープアライブ間隔 (秒)。ピアの活動状態を確認するために、構成された間隔でキープアライブ・メッセージを送信します。範囲: 5 秒から 86399 秒。デフォルト値は `15` 秒です。

-ike *NAME* (オプション): IKE ポリシーの名前。

-ipsec *NAME* (オプション): IPSec ポリシーの名前。

**例**:

`my_connection` という名前の新しい VPN 接続を作成します:

```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
IKE ポリシーを作成します。

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必須): IKE ポリシーの名前。

-g *GATEWAY_NAME* (必須): ゲートウェイの名前。

-d *DESCRIPTION* (オプション): 指定されたパラメーターの説明。

-pfs *GROUP* (オプション): Diffie-Hellman (DH) グループ ID。有効な値は、`Group2`、`Group5`、または `Group14` です。デフォルト値は `Group2` です。

-e *ENCRYPTION_ALGORITHM* (オプション): 暗号化アルゴリズム。有効な値は、`aes-128`、`aes-192`、`aes-256`、または `3des` です。デフォルト値は `aes-128` です。

-lv *LIFETIME_VALUE* (オプション): IKE セキュリティー・アソシエーションの存続時間値。範囲: 60 秒から 86400 秒。デフォルト値は `86400` 秒です。

**例**:

`my_ike` という名前の新しい IKE ポリシーを作成します:

```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
IPSec ポリシーを作成します。

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必要): IPSec ポリシーの名前。

-g *GATEWAY_NAME* (必須): ゲートウェイの名前。

-d *DESCRIPTION* (オプション): 指定されたパラメーターの説明。

-pfs *GROUP* (オプション): Diffie-Hellman (DH) グループ ID。有効な値は、`Group2`、`Group5`、または `Group14` です。デフォルト値は `Group2` です。

-e *ENCRYPTION_ALGORITHM* (オプション): 暗号化アルゴリズム。有効な値は、`aes-128`、`aes-192`、`aes-256`、または `3des` です。デフォルト値は `aes-128` です。

-lv *LIFETIME_VALUE* (オプション): セキュリティー・アソシエーションの存続時間値。範囲: 60 秒から 86400 秒。デフォルト値は `3600` 秒です。

**例**:

`my_policy` という名前で IPSec ポリシーを作成します。

```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
VPN ゲートウェイを作成します。

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*GATEWAY_NAME* (必須): ゲートウェイの名前。

-t *TYPE* (必須): サービスを有効にするコンテナー。有効な値は、`allSingleContainers`、`allContainerGroups`、または `allContainers` です。 デフォルト値はありません。タイプを指定する必要があります。

-gateway_ip *IP_ADDRESS* (オプション): ゲートウェイの IP アドレス。

-subnets *SUBNET_ADDRESS* (オプション): CIDR 形式のサブネット・アドレス。

**例**:

名前が `my_gateway` で、タイプが `allContainerGroups` のゲートウェイを作成します。

```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
現在の接続すべてについての情報が表示されます。

```
bluemix vpn connections
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix vpn ikes
現在の IKE 接続についての情報が表示されます。

```
bluemix vpn ikes
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix vpn ipsecs
現在の IPSec 接続についての情報が表示されます。

```
bluemix vpn ipsecs
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix vpn gateways
現在のゲートウェイについての情報が表示されます。

```
bluemix vpn gateways
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix vpn connection
特定の接続についてのすべての情報が表示されます。

```
bluemix vpn connection CONNECTION_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CONNECTION_NAME* (必須): 表示される接続の名前。


## bluemix vpn ike
IKE 接続についての情報が表示されます。

```
bluemix vpn ike POLICY_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必須): 表示される IKE ポリシーの名前。


## bluemix vpn ipsec
IPSec 接続についての情報が表示されます。

```
bluemix vpn ipsec POLICY_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必須): 表示される IPSec ポリシーの名前。


## bluemix vpn gateway
ゲートウェイについての接続情報が表示されます。

```
bluemix vpn gateway GATEWAY_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*GATEWAY_NAME* (必須): 表示されるゲートウェイの名前。


## bluemix vpn connection-delete
既存の接続を削除します。

```
bluemix vpn connection-delete CONNECTION_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CONNECTION_NAME* (必須): 削除される接続の名前。


## bluemix vpn ike-delete
既存の IKE ポリシーを削除します。

```
bluemix vpn ike-delete POLICY_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必須): 削除される IKE ポリシーの名前。


## bluemix vpn ipsec-delete
既存の IPSec ポリシーを削除します。

```
bluemix vpn ipsec-delete POLICY_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必須): 削除される IPSec ポリシーの名前。


## bluemix vpn gateway-delete
既存のゲートウェイを削除します。

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*GATEWAY_NAME* (必須): 削除されるゲートウェイの名前。


## bluemix vpn connection-update
既存の VPN 接続を更新します。

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME] [-k PRESHARED_KEY] [-subnets "SUBNET/MASK"] [-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CONNECTION_NAME* (必須): 接続の名前。

-g *GATEWAY_NAME* (オプション): ゲートウェイの名前。

-k *PRESHARED_KEY* (オプション): 事前共有鍵。

-subnets "*SUBNET*/*MASK*" (オプション): CIDR 形式のサブネット・アドレス。

-cip *CUSTOMER_GATEWAY_IP_ADDRESS* (オプション): VPN トンネルのリモート・エンドポイント IP アドレス。

-d *DESCRIPTION* (オプション): 指定されたパラメーターの説明。

-peer_id *PEER_ID* (オプション): リモート・ピアの ID。VPN トンネルの相手側のエンドポイント。

-admin_state *ADMIN_STATE* (オプション): VPN 接続の状況。有効な値は、`UP` または `DOWN` です。

-dpd-action *ACTION* (オプション): ピアが非活動として検出された場合に取るアクション。有効な値は、`hold`、`clear`、`disabled`、`restart`、または `restart-by-peer` です。

-gateway_ip *IP_ADDRESS* (オプション): ローカル VPN トンネル・エンドポイントの IP アドレス。

-i *INITIATOR_STATE* (オプション): イニシエーターの状態。

-dpd-timeout *VALUE* (オプション): セッションが終了するまでのタイムアウト値 (秒)。範囲: 6 秒から 86400 秒。

-dpd-interval *VALUE* (オプション): キープアライブ間隔 (秒)。ピアの活動状態を確認するために、構成された間隔でキープアライブ・メッセージを送信します。範囲: 5 秒から 86399 秒。

-ike *NAME* (オプション): IKE ポリシーの名前。

-ipsec *NAME* (オプション): IPSec ポリシーの名前。


## bluemix vpn ike-update
IKE ポリシーを更新します。

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必須): IKE ポリシーの名前。

-g *GATEWAY_NAME* (オプション): ゲートウェイの名前。

-d *DESCRIPTION* (オプション): 指定されたパラメーターの説明。

-pfs *GROUP* (オプション): Diffie-Hellman (DH) グループ ID。有効な値は、`Group2`、`Group5`、または `Group14` です。

-e *ENCRYPTION_ALGORITHM* (オプション): 暗号化アルゴリズム。有効な値は、`aes-128`、`aes-192`、`aes-256`、または `3des` です。

-lv *LIFETIME_VALUE* (オプション): IKE セキュリティー・アソシエーションの存続時間値。範囲: 60 秒から 86400 秒。


## bluemix vpn ipsec-update
IPSec ポリシーを更新します。

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*POLICY_NAME* (必要): IPSec ポリシーの名前。

-g *GATEWAY_NAME* (オプション): ゲートウェイの名前。

-d *DESCRIPTION* (オプション): 指定されたパラメーターの説明。

-pfs *GROUP* (オプション): Diffie-Hellman (DH) グループ ID。有効な値は、`Group2`、`Group5`、または `Group14` です。

-e *ENCRYPTION_ALGORITHM* (オプション): 暗号化アルゴリズム。有効な値は、`aes-128`、`aes-192`、`aes-256`、または `3des` です。

-lv *LIFETIME_VALUE* (オプション): セキュリティー・アソシエーションの存続時間値。範囲: 60 秒から 86400 秒。


## bluemix vpn gateway-update
既存の VPN ゲートウェイを更新します。

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE] [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*GATEWAY_NAME* (必須): ゲートウェイの名前。

-t *TYPE* (オプション): サービスを有効にするコンテナー。有効な値は、`allSingleContainers`、`allContainerGroups`、または `allContainers` です。 

-gateway_ip *IP_ADDRESS* (オプション): ゲートウェイの IP アドレス。

-subnets *SUBNET_ADDRESS* (オプション): CIDR 形式のサブネット・アドレス。
