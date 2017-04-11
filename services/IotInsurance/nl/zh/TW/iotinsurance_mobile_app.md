---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 安裝及連接範例行動應用程式
{: #iot4i_gettingstarted}

{{site.data.keyword.iotinsurance_full}} 範例行動應用程式是 {{site.data.keyword.iotinsurance_short}} 行動用戶端的參照實作。您可以使用應用程式在系統中登錄新裝置，以及接收裝置的警示。
{:shortdesc}

**附註**：{{site.data.keyword.iotinsurance_short}} 不再部署 {{site.data.keyword.amafull}} 或 {{site.data.keyword.mobilepushfull}}。較舊版的 {{site.data.keyword.iotinsurance_short}} 使用 {{site.data.keyword.amashort}} 服務來處理來自行動應用程式的回應。這個處理程序仍然適用於所有現有的 {{site.data.keyword.iotinsurance_short}} 實例。不過，您必須建立自訂鑑別處理程序，才能使用行動應用程式搭配新的
{{site.data.keyword.iotinsurance_short}} 實例。您也可以選擇性地[建立 {{site.data.keyword.mobilepushshort}} 實例](../mobilepush/index.html)、配置它，然後將它連結至 {{site.data.keyword.iotinsurance_short}} API。

**必要條件：**開始之前，請確定已具有下列必要條件：
  - Apple Xcode 8 或以上版本的整合開發環境。
  - iOS 9.0 或以上版本的 iPhone 行動裝置。
  - 電腦上所安裝的 CocoaPods。請參閱 [CocoaPods 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://guides.cocoapods.org/using/getting-started.html){: new_window}。
  - 將範例行動應用程式連接至服務實例所需的[參數](#iot4i_mobileParam)。

## 建置範例行動應用程式
{: #building_mobile}
若要嘗試範例行動應用程式，請執行下列作業：

1. 將[範例行動應用程式的原始碼儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){: new_window} 複製至已安裝 Xcode 7.3 或以上版本的電腦。
2. 在專案上執行 CocoaPods pod install 指令，以安裝必要套件，並產生 IoT4I.xcworkspace 檔案。必須安裝 CocoaPods，才能完成此作業。
3. 按兩下 IoT4I.xcworkspace 檔案，以在 Xcode 中開啟專案。
4. 將 iPhone 連接至電腦，並將它選取為建置目的地。
5. 在檔案清單中選取 IoT4I 檔案，以顯示「身分」對話框。
6. 在 Xcode 的「身分」對話框中，進行下列變更：
  - 將**軟體組 ID** 變更為唯一 ID（例如：**myIoT4Ibundle**）。
  - 將**團隊**設為您的個人群組名稱，然後按一下**修正問題**。
7. 若要將應用程式連接至 {{site.data.keyword.iotinsurance_short}} 實例，請在 **constants.swift** 檔案中設定下列參數：  
    - [applicationRoute](#iot4i_mobileParam) = {{site.data.keyword.iotinsurance_short}} API 應用程式的 URL。您可以在 {{site.data.keyword.iotinsurance_short}} 服務主控台的「服務認證」標籤找到這個值。
    - [applicationId](#iot4i_mobileParam) = {{site.data.keyword.amashort}} 實例的 GUID。您可以開啟 {{site.data.keyword.amashort}}，然後按一下**行動選項**，找到這個值。值稱為應用程式 GUID / 承租戶 ID。
8. 在您的電腦上，按一下箭頭以建置並執行現行架構。即會在手機上安裝範例行動應用程式。如需相關資訊，請參閱[透過 Xcode 在裝置上執行應用程式的 Apple 開發人員指示 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html){: new_window}。

  **附註：**如果在您嘗試建置時顯示*無法啟動 IoT4I，因為您尚未驗證裝置上已信任「開發人員應用程式」憑證*錯誤，請將您自己選取為「授信開發人員」，如下所示：  
    1. 在手機上，移至**設定 > 一般 > 裝置管理 > yourDeveloperID**。
    2. 點選開發人員 ID 帳戶名稱，以建立開發人員 ID 的信任。
    3. 系統提示時，確認已信任開發人員 ID。

## 啟用行動應用程式的推送通知
{: #iot4i_pushNotification}

執行下列作業，以啟用行動裝置的推送通知。您必須具有有效的「Apple 開發人員帳戶」成員資格，才能使用 Push Notification Service。

1. 登入您的 [Apple 開發人員帳戶 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.apple.com/account){: new_window}。

2. 建立憑證檔案。
  1. 選取**憑證、ID 及設定檔**。
  2. 選取「ID：應用程式 ID」。
  3. 按一下「新增」按鈕 (+) 以建立新的「應用程式 ID」。
  4. 在**說明**中，輸入「應用程式」的說明。
  5. 選取**明確應用程式 ID**，然後輸入軟體組 ID（例如 com.YourOrganizationName.iot4i.mobileApp）。
  6. 在**推送通知**上選取 (V)，然後按一下**繼續 > 登錄 > 完成**。

3. 建立推送通知憑證。
  1. 選取**憑證：全部**。
  2. 按一下「新增」按鈕 (+) 以建立新的 APN 憑證。
  3. 在「新增 iOS 憑證」頁面中，選取 **Apple Push Notification Service SSL（沙盤推演）**，然後按一下**繼續**。
  4. 選取您在前一個步驟中建立的「應用程式 ID」，然後按一下**繼續**。
  5. 使用頁面上的指示來建立 CSR 檔案，然後按一下**繼續**。
  6. 選取您建立的 CSR 檔案，然後按一下**繼續**。
  7. 下載並執行憑證檔案。

4. 建立設定檔。
  1. 選取**佈建設定檔：開發**。
  2. 按一下「新增」按鈕 (+) 以建立新的開發設定檔。
  3. 選取 **iOS 應用程式開發**，然後按一下**繼續**。
  4. 選取您先前建立的「應用程式 ID」。
  5. 選取**開發人員憑證：全部**，然後按一下**繼續**。
  5. 選取**所有開發裝置（測試裝置）**，然後按一下**繼續**。
  6. 指定「設定檔名稱」，然後按一下**繼續**。
  7. 下載並執行所產生的設定檔。

5. 建立「公開金鑰密碼化標準 (PKCS) 12」檔案，並將它新增至 {{site.data.keyword.mobilepushshort}} 服務。
  1. 開啟「金鑰鏈存取」，然後選取**我的憑證**。
  2. 在 **Apple 開發 IOS Push 服務：(bundleID)** 上按一下滑鼠右鍵，然後匯出、儲存及輸入檔案的密碼。
  3. 在您的 {{site.data.keyword.Bluemix_notm}} 主控台中，開啟 {{site.data.keyword.mobilepushshort}} 服務。
  4. 按一下**配置**。
  5. 在「Apple Push Notifications 憑證」區段中，上傳 PKCS 12 檔案，然後輸入密碼。
  6. 在 Xcode 中，將軟體組 ID 變更為您先前建立的軟體組 ID。
  7. 執行應用程式，並授與 Push Notification 服務的許可權。
