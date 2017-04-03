---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービスに置き換えられます。

# カスタム認証用の {{site.data.keyword.amashort}} の構成
{: #custom-dash}


モバイル・アプリケーションでカスタム認証を使用するには、{{site.data.keyword.amashort}} サービス・ダッシュボードで、カスタム ID プロバイダーのカスタム認証レルムとベース URL を登録する必要があります。

## 開始する前に
{: #custom-dash-begin}
以下が必要です。
* {{site.data.keyword.amafull}} サービスのインスタンス。
* カスタム ID プロバイダー・アプリケーション。

## {{site.data.keyword.amafull}} ダッシュボードでのカスタム認証の構成
{: #custom-dash-config}
{{site.data.keyword.amafull}} ダッシュボードを使用してカスタム認証を構成します。

1. {{site.data.keyword.amafull}} ダッシュボードでサービスを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
1. **「カスタム」**セクションを展開します。
1. **「レルム名」**、**「カスタム ID プロバイダー URL」**を入力します。**「Web アプリケーションのリダイレクト URI (Your Web Application Redirect URIs)」**値は、Web アプリケーションの場合にのみ必要です。

## 次のステップ
{: #next-steps}
* [Android 用のカスタム認証の構成 ](custom-auth-android.html)
* [iOS 用のカスタム認証の構成 ](custom-auth-ios-swift-sdk.html)
* [Cordova 用のカスタム認証の構成 ](custom-auth-cordova.html)
