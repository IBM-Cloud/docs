---



copyright:

  years: 2015，2017

lastupdated: "2016-03-15"


---

{:shortdesc: .shortdesc}

# VCAP サービス


VCAP_SERVICES 環境変数は、{{site.data.keyword.Bluemix_notm}} でサービス・インスタンスと対話するために使用できる情報が格納された JSON オブジェクトです。
{:shortdesc}


## VCAP_SERVICES 環境変数の値の取得
{:retrieving}

VCAP_SERVICES 環境変数は、{{site.data.keyword.Bluemix_notm}} でサービス・インスタンスと対話するために使用できる情報が格納された JSON オブジェクトです。この情報には、サービス・インスタンス名、資格情報、およびサービス・インスタンスへの接続 URL が含まれています。これらの値は、アプリケーションが {{site.data.keyword.Bluemix_notm}} でサービス・インスタンスにバインドされると VCAP_SERVICES 環境変数に取り込まれます。

VCAP_SERVICES 環境変数の値は、サービス・インスタンスをアプリケーションにバインドしたときにのみ使用可能です。アプリケーション環境変数は、以下のコマンドを使用して表示できます。

```
cf env APP_NAME
```
