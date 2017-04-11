---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}} 概説
{: #gettingstartedtemplate}
最終更新日: 2017 年 1 月 19 日
{: .last-updated}

{:shortdesc}

{{site.data.keyword.mobilepushshort}} は、モバイル・カテゴリー内の Bluemix カタログ・サービスとして使用可能であり、モバイルおよび Web のプッシュ通知の送信と管理を可能にします。このサービスは、通知のディスパッチを処理しながら、アプリケーション・ユーザーとデバイス、デバイス・プラットフォーム、および Web ブラウザーとのマッピングを管理します。

 {{site.data.keyword.mobilepushshort}} は、MobileFirst Services Starter ボイラープレートの一部として、および Bluemix [専用サービス](/docs/dedicated/index.html)として使用可能です。このサービスを使用して、ブロードキャスト、ユニキャスト (deviceID と userID に基づく)、タグ・ベースの通知、Web フックベースの通知だけでなく、リッチ・メディア通知と対話式通知もモバイル・ユーザーと Web ブラウザー・アプリケーション・ユーザーに送信することができます。また、SDK (Software Development Kit) と [REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を使用して、クライアント・アプリケーションをさらに開発することもできます。

このサービスでは、ユーザー・データからグラフおよびレポートを生成してプッシュ通知のパフォーマンスのモニターに役立つモニタリング機能も提供されています。[プッシュ通知のモニター](/docs/services/mobilepush/t_push_monitoring.html)を参照してください。

{{site.data.keyword.mobilepushshort}} サービスは、以下のプラットフォームでサポートされています。

- [iOS および Android のモバイル・デバイス](/docs/services/mobilepush/c_enable_push.html)
- [Google Chrome、Mozilla Firefox、および Safari の Web ブラウザー](/docs/services/mobilepush/c_chrome_firefox_enable.html)
- [Google Chrome アプリケーションおよびエクステンション](/docs/services/mobilepush/c_web_extensions.html)


# 関連リンク
{: #rellinks}

* [概要![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](c_overview_push.html){: new_window}

## チュートリアルおよびサンプル {:id="samples"}
{: #samples}
* [Android helloPush のサンプル・アプリケーション![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [Cordova のサンプル・アプリケーション![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [iOS helloPush のサンプル・アプリケーション (Swift) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellopush){: new_window}

## SDK
{: #sdk}
* [Android SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Cordova SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [iOS SDK (Swift) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/zip/master){: new_window}

## API リファレンス
{: #api}
* [Push API リファレンス (Android) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [BMS Push API リファレンス iOS (Swift) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/blob/development/Apple Docs/index.html){: new_window}
* [REST API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}
