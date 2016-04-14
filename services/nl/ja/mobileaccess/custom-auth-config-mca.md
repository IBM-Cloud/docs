---

copyright:
  years: 2015, 2016
  
---

# カスタム認証用の {{site.data.keyword.amashort}} の構成
{: #custom-dash}
モバイル・アプリケーションでカスタム認証を使用するには、{{site.data.keyword.amashort}} サービス・ダッシュボードで、カスタム ID プロバイダーのカスタム認証レルムとベース URL を登録する必要があります。

## 開始する前に
{: #custom-dash-begin}
* [入門](getting-started.html)をお読みください。
* {{site.data.keyword.amashort}} Server SDK でバックエンド・アプリケーションを保護します。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。
* カスタム ID プロバイダー・アプリケーションを実行します。

## {{site.data.keyword.Bluemix}} ダッシュボードでのカスタム認証の構成
{: #custom-dash-config}
{{site.data.keyword.amashort}} ダッシュボードを使用してカスタム認証を構成します。

1. {{site.data.keyword.Bluemix}}ダッシュボードでアプリを開きます。

1. **「モバイル・オプション」**をクリックし、**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

1. **「カスタム」**タイルをクリックします。

1. カスタム ID プロバイダーの**「レルム名」**と**「ベース URL」** を入力し、変更内容を保存します。

## 次のステップ
{: #next-steps}
* [Android 用のカスタム認証の構成 ](custom-auth-android.html)
* [iOS 用のカスタム認証の構成 ](custom-auth-ios.html)
* [Cordova 用のカスタム認証の構成 ](custom-auth-cordova.html)
