---

copyright:
  years: 2015, 2016
  
---

# 配置 {{site.data.keyword.amashort}} 進行自訂鑑別
{: #custom-dash}
若要搭配使用自訂鑑別與行動式應用程式，您必須在 {{site.data.keyword.amashort}} 服務儀表板中登錄自訂鑑別領域，以及自訂身分提供者的基本 URL。

## 開始之前
{: #custom-dash-begin}
* 閱讀[開始使用](getting-started.html)。
* 使用 {{site.data.keyword.amashort}} Server SDK 保護後端應用程式。如需相關資訊，請參閱[保護資源](protecting-resources.html)。
* 讓自訂身分提供者應用程式執行。

## 在 {{site.data.keyword.Bluemix}} 儀表板中配置自訂鑑別
{: #custom-dash-config}
使用 {{site.data.keyword.amashort}} 儀表板來配置自訂鑑別。

1. 在 {{site.data.keyword.Bluemix}} 儀表板中開啟應用程式。

1. 按一下**行動式選項**，並記下您的**路徑** (`applicationRoute`) 及 **應用程式 GUID** (`applicationGUID`)。起始設定 SDK 時，您需要這些值。

1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。

1. 按一下**自訂**磚。

1. 輸入自訂身分提供者的**領域名稱**及**基本 URL**，並儲存變更。

## 後續步驟
{: #next-steps}
* [配置適用於 Android 的自訂鑑別](custom-auth-android.html)
* [配置適用於 iOS 的自訂鑑別](custom-auth-ios.html)
* [配置適用於 Cordova 的自訂鑑別](custom-auth-cordova.html)
