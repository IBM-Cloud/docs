---

copyright:
  years: 2015, 2016

---

# 入門
{: #getting-started}
{{site.data.keyword.amashort}} の使用を開始するには、{{site.data.keyword.amashort}} サービスを既存の {{site.data.keyword.Bluemix}} アプリケーションに追加するか、ボイラープレートを使用して新しいアプリを作成することができます。  

## {{site.data.keyword.amashort}} サービスのインスタンスの作成
{: #service-instance}

{{site.data.keyword.Bluemix}} カタログから {{site.data.keyword.amashort}} サービスの新しいインスタンスを作成できます。新しいモバイル・バックエンドを作成するためにボイラープレートを使用しない場合は、既存のバックエンドに Server SDK を構成する必要があります。


  * **新規アプリ**: 以下のセクションの説明では、モバイル・バックエンドを作成し、{{site.data.keyword.amashort}} Server SDK を使用して保護する新規アプリの作成方法について説明します。**MobileFirst Services Starter** ボイラープレートをクリックして、{{site.data.keyword.amashort}} サービスで新しいアプリケーションを作成します。
  * **既存のアプリ**: {{site.data.keyword.amashort}} アイコンをクリックし、既存のアプリケーションにバインドされた新規サービス・インスタンスを作成します。既存のアプリに Server SDK を構成するには、[クラウド・リソースの保護](protecting-resources.html)を参照してください。


## MobileFirst Services Starter ボイラープレートを使用したモバイル・バックエンドの作成
{: #create-backend}
MobileFirst Services Starter を使用すると、IBM {{site.data.keyword.Bluemix_notm}} 上で稼働してカスタム・バックエンド・ロジックを実装する Node.js ランタイムのインスタンスを取得します。セキュリティー、データ、プッシュ、およびモニターの各機能を提供する一連のコア・モバイル・サービスは、その Node.js アプリにバインドされています。{{site.data.keyword.Bluemix_notm}} Node.js アプリが作成されたら、 開発環境をセットアップし、{{site.data.keyword.Bluemix_notm}} モバイル・サービスの SDK の使用を開始できます。SDK を使用すると、単純な API 呼び出しを使用して、クラウド・アプリにバインドされているサービスにアクセスできます。

1. {{site.data.keyword.Bluemix_notm}} カタログから、**「ボイラープレート」**セクションに移動し、**「MobileFirst Services Starter」**をクリックします。
1. スペース、名前、ホスト、およびサービス・プランなどの、モバイル・バックエンドに関する情報を追加します。
1. **「作成」**をクリックします。



## 次のステップ
{: #next-steps}
ボイラープレートを使用して作成した Node.js アプリケーションのいくつかのエンドポイントは、{{site.data.keyword.amashort}} によって保護されています。デフォルトのモバイル・バックエンド・アプリケーションについて詳しく知りたい場合は、[bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop) を参照してください。

{{site.data.keyword.amashort}} SDK を使用するようにモバイル・アプリをセットアップすることができます。SDK をセットアップしたら、ご使用のアプリでの認証およびモニタリングのセットアップを開始できます。ご使用のモバイル開発プラットフォーム用の説明に従ってください。

* [Android](getting-started-android.html)
* [iOS (Swift SDK)](getting-started-ios.html)
* [iOS (Objective-C SDK)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
