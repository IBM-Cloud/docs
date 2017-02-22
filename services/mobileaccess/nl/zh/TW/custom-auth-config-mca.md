---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

# 配置 {{site.data.keyword.amashort}} 進行自訂鑑別
{: #custom-dash}


若要搭配使用自訂鑑別與行動應用程式，您必須在 {{site.data.keyword.amashort}} 服務儀表板中登錄自訂身分提供者的自訂鑑別領域以及基本 URL。

## 開始之前
{: #custom-dash-begin}
您必須具有：
* {{site.data.keyword.amafull}} 服務的實例。
* 自訂身分提供者應用程式。

## 在 {{site.data.keyword.amafull}} 儀表板中配置自訂鑑別
{: #custom-dash-config}
使用 {{site.data.keyword.amafull}} 儀表板來配置自訂鑑別。

1. 在 {{site.data.keyword.amafull}} 儀表板中，開啟服務。
1. 在**管理**標籤中，將**授權**切換為開啟。
1. 展開**自訂**區段。
1. 輸入**領域名稱**、**自訂身分提供者 URL**。只有 Web 應用程式需要**您的 Web 應用程式重新導向 URI** 值。

## 後續步驟
{: #next-steps}
* [配置 Android 應用程式的自訂鑑別](custom-auth-android.html)
* [配置適用於 iOS 的自訂鑑別](custom-auth-ios-swift-sdk.html)
* [配置 Cordova 應用程式的自訂鑑別](custom-auth-cordova.html)
