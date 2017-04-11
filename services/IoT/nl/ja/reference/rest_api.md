---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# API
{: #overview}

{{site.data.keyword.iot_full}} に接続するデバイス、ゲートウェイ、アプリケーション向けのコードの開発用に、いくつかの API を使用できます。

HTTP API は、HTTP 基本認証で保護されています。ダッシュボードを使用して API キーを生成すると、キーと認証トークンが提示されます。詳しくは、次を参照してください。


## HTTP REST API

対象の組織の登録を行うと、6 文字の組織 ID が提示されます。この ID は、すべての API 呼び出しのホスト名で必要になります。組織のベース URL には、以下のアドレスでアクセスできます。

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002/

アプリケーション API に対する要求を認証するには、ユーザー名を API キーに設定し、パスワードを認証トークンに設定します。

Messaging API の場合は、次のアドレスを使用してください。https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002


## API リンク

次の表のリンクを使用して、{{site.data.keyword.iot_short_notm}} に用意されている API の詳細を参照してください。

### 汎用 HTTP API

API                     | 使用目的       
------------- | -------------
[組織管理 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | 組織を構成し (デバイスの作成と削除を含む)、使用量とサービス状況を確認し、デバイス接続の問題を診断します。
[セキュリティー ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | ユーザーの招待および認証と、ユーザー、API キー、およびデバイスの権限を管理します。
[情報管理 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  デバイス・イベント・データにアクセスし、デバイス・ロケーションを取得および更新し、そのロケーションの気象情報を取得します。**注:** 気象情報は、The Weather Company の統合に依存しています。
[The Weather Company ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | The Weather Company からのデータを既存のデバイスに統合します。
[分析 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/analytics.html){: new_window} | デバイスから {{site.data.keyword.iot_short_notm}} に入るデータに対するルール、アラート、アクションを作成します。
[デバイス管理 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/device-mgmt.html){: new_window} | デバイス管理プロトコルを使用して、管理対象デバイスとやり取りします。
[メッセージング ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | HTTP を使用して、イベントをパブリッシュし、コマンドを送信します。**注:** Messaging API の場合は、次のアドレスを使用してください。https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002



### 拡張 HTTP API

API                     | 使用目的       
------------- | -------------
[AT&T 拡張 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | AT&T デバイスを管理します。
[Jasper 拡張 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Jasper デバイスを管理します。
[Orange 拡張 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | {{site.data.keyword.iot_short_notm}} 組織に接続されている Orange SIM カード装着デバイスの SIM カード・データを表示します。

### ベータ HTTP API

API                     | 使用目的       
------------- | -------------
[ゲートウェイ・セキュリティー ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | ゲートウェイ・デバイスを検査し、それに役割を割り当てます。
[デバイス・セキュリティー ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | デバイスを検査して役割を割り当てます。
[インターフェース・マッピング ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   インターフェースを使用してデバイス・データをマップし、それにアクセスします。
