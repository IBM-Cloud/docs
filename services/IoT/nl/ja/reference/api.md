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
{: #api_overview}

{{site.data.keyword.iot_full}} に接続するデバイス、ゲートウェイ、アプリケーション向けのコードの開発用に、いくつかの API を使用できます。

HTTP API は、HTTP 基本認証で保護されています。ダッシュボードを使用して API キーを生成すると、キーと認証トークンが提示されます。API キーとトークンについて詳しくは、[API キー接続](../platform_authorization.html#api-key)を参照してください。


## HTTP API について
{: #api_about}

対象の組織の登録が済むと、すべての HTTP API 呼び出しのホスト名で必要な、6 文字の組織 ID が提示されます。組織のベース URL には、以下のアドレスでアクセスできます。

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002

アプリケーション API に対する要求を認証するには、ユーザー名を API キーに設定し、パスワードを認証トークンに設定します。

Messaging API の場合は、以下のアドレスを使用します。

https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002

## HTTP API
{: #api_http}

API                     | 使用目的       
------------- | -------------
[組織管理 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | 組織を構成し (デバイスの作成と削除を含む)、使用量とサービス状況を確認し、デバイス接続の問題を診断します。
[セキュリティー ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | ユーザーの招待および認証と、ユーザー、API キー、およびデバイスの権限を管理します。
[情報管理 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  デバイス・イベント・データにアクセスし、デバイス・ロケーションを取得および更新し、そのロケーションの気象情報を取得します。
[デバイス管理 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/deviceMgmt.html){: new_window} | デバイス管理プロトコルを使用して、管理対象デバイスとやり取りします。
[メッセージング ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | HTTP を使用して、イベントをパブリッシュし、コマンドを送信します。**注:** Messaging API の場合は、次のアドレスを使用してください。*https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002*



## 拡張 HTTP API
{: #api_extension}

API                     | 使用目的       
------------- | -------------
[AT&T 拡張 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | AT&T デバイスを管理します。
[Jasper 拡張 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Jasper デバイスを管理します。
[Orange 拡張 ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | {{site.data.keyword.iot_short_notm}} 組織に接続されている Orange SIM カード装着デバイスの SIM カード・データを表示します。

## ベータ HTTP API
{: #api_beta}

API                     | 使用目的       
------------- | -------------
[ゲートウェイ・セキュリティー ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | ゲートウェイ・デバイスを検査し、それに役割を割り当てます。
[デバイス・セキュリティー ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | デバイスを検査して役割を割り当てます。
[インターフェース・マッピング ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   インターフェースを使用してデバイス・データをマップし、それにアクセスします。
