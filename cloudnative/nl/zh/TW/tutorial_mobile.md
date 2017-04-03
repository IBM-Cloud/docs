---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Mobile Basic Starter 的完整指導教學
{: #tutorial}

下列完整指導教學逐步執行從 Mobile Basic Starter 建立專案的步驟，包括您必須安裝的工具，以及在 Xcode 及 Android Studio 中執行專案的步驟。


## 安裝開發人員工具
{: #dev_tools}

請確定您已安裝[必備開發人員工具 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](get_code.html#prereq-dev-tools){: new_window}。


## 使用 {{site.data.keyword.dev_console}} 建立專案
{: #create-devex}

1. 在 {{site.data.keyword.Bluemix}} 中，建立 {{site.data.keyword.dev_console}} 專案。

   1. 從 {{site.data.keyword.dev_console}} 的**開始使用**頁面中，按一下**建立專案**。

      您也可以按一下**專案**頁面中的**建立專案**。

   2. 選取 **Mobile App**，然後按**下一步**。

   3. 選取 **Basic**，然後按**下一步**。

   4. 輸入專案名稱。對於此指導教學，使用 `MobileBasicProject`。

   5. 選取平台。對於此指導教學，使用 `Swift`。
   
   6. 按一下**建立**。

2. 選用項目：新增「鑑別」功能。

   1. 在**專案概觀**頁面上，針對**鑑別**按一下**新增**。

      您也可以選取**功能 > 鑑別**頁面上的**建立**或**新增現有項目**。

   2. 輸入服務名稱，然後按一下**建立**。
   
   3. 開啟**鑑別**。
   
   4. 選取您的身分提供者，並且輸入必要資訊以進行配置。您只能啟用一個身分提供者。
   
   5. 如需配置「鑑別」的相關資訊，請參閱[配置身分提供者 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/appid/identity-providers.html){: new_window}。

3. 選用項目：新增分析功能。

   1. 在**專案概觀**頁面中，針對**分析**按一下**新增**。

      您也可以按一下**功能 > 分析**頁面中的**建立**或**新增現有項目**。

   2. 輸入服務名稱，然後按一下**建立**。
   
   3. 在您執行應用程式之後，即可關閉**展示模式**來查看分析資料。
   
   4. 如需配置分析的相關資訊，請參閱[開始使用 {{site.data.keyword.mobileanalytics_short}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/index.html){: new_window}。

4. 選用項目：新增 {{site.data.keyword.mobilepushshort}} 功能。

   1. 在**專案概觀**頁面中，對 **{{site.data.keyword.mobilepushshort}}** 按一下**新增**。

      您也可以按一下**功能 > {{site.data.keyword.mobilepushshort}}** 頁面中的**建立**或**新增現有項目**。

   2. 輸入服務名稱，然後按一下**建立**。

   3. 若為 iOS，請[配置 Apple Push Notification Service ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}。

   4. 若為 Android，請[配置 Firebase Cloud Messaging ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}。

5. 選用項目：新增資料功能。

   1. 在**專案概觀**頁面上，針對**資料**按一下**檢視**。

      您也可以選取**資料**頁面上的**建立**。
      
   2. 選擇 **{{site.data.keyword.cloudant_short_notm}}** 或 **{{site.data.keyword.objectstorageshort}}**。

   3. 輸入服務名稱，然後按一下**建立**。

   4. 如需配置 {{site.data.keyword.cloudant_short_notm}} 的相關資訊，請參閱[開始使用 {{site.data.keyword.cloudant_short_notm}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/Cloudant/index.html){: new_window}。

   5. 如需配置 {{site.data.keyword.objectstorageshort}} 的相關資訊，請參閱[開始使用 {{site.data.keyword.objectstorageshort}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/ObjectStorage/index.html){: new_window}。

6. 產生專案程式碼。

   1. 按一下**專案概觀**頁面上的**取得程式碼**，以選取您的語言。
   
      您也可以按一下**程式碼**頁面。
      
   2. 按一下**產生 Swift**。
   
   3. 專案程式碼產生完成後，請按一下**下載 Swift** 來下載專案保存檔。

7. 選用項目：[更新專案](project_overview_page.html#update_language)以產生新語言。


## 使用 {{site.data.keyword.dev_cli_notm}} 建立專案
{: #create-cli}

1. 確定您已安裝 [{{site.data.keyword.dev_cli_short}}](dev_cli.html)。

2. 在「終端機」提示字元中，導覽至您選擇的本端目錄，然後執行下列指令。

	```
	bx dev create
	```
	{: codeblock}
	
3. 系統提示時，提供下列值：

	* 選取型樣：2（適用於 Mobile）
	* 選取入門範本：1（適用於 Basic）
	* 選取平台：3（適用於 iOS Swift）
	* 輸入專案的名稱：`MobileBasicProjectCLI`

4. 如果您要將服務新增至專案，請在問題提示字元中鍵入 `y`，並回答其餘的問題。

5. 順利儲存 `MobileBasicProjectCLI` 後，請導覽至 `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift` 資料夾。


## 在 Xcode 中執行 Swift 專案
{: #run_swift}

1. 解壓縮 `MobileBasicProject-Swift.zip` 檔案。

2. 在 Markdown 檢視器中開啟 `README.md` 檔案，以檢閱配置專案的步驟。

   1. 開啟終端機，然後導覽至您的專案資料夾。
   
      1. 如果您需要設定 CocoaPods 儲存庫，請執行 `pod setup`。
      
      2. 如果您需要更新現有 Pods，請執行 `pod update`。
      
      3. 執行 `pod install`，以安裝您專案所需的 Pods。
      
   3. 開啟 `BasicProject.xcworkspace` Xcode 工作區。
      
3. 執行應用程式。


## 在 Xcode 中執行 Cordova 專案
{: #run_cordova_xcode}

1. 解壓縮 `MobileBasicProject-Cordova.zip` 檔案。

2. 在 Markdown 檢視器中開啟 `README.md` 檔案，以配置專案。

   1. 在 Xcode 中開啟 `platforms/ios` 專案。
      
3. 執行應用程式。


## 在 Android Studio 中執行 Cordova 專案
{: #run_cordova_studio}

1. 解壓縮 `BasicProject-Cordova.zip` 檔案。

2. 在 Markdown 檢視器中開啟 `README.md` 檔案，以配置專案。

   1. 在 Android Studio 中開啟 `platforms/android` 專案。
      
3. 執行應用程式。


## 在 Android Studio 中執行 Android 專案
{: #run_android}

1. 解壓縮 `MobileBasicProject-Android.zip` 檔案。

2. 在 Markdown 檢視器中開啟 `README.md` 檔案，以配置專案。

   1. 在 Android Studio 中開啟 `BasicProject-Android` 專案。
      
3. 執行應用程式。
