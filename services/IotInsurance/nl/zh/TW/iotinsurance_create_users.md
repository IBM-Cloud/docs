---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 建立使用者與防護的關聯
{: #gettingstartedtemplate}
前次更新：2016 年 9 月 15 日
{: .last-updated}

建立 {{site.data.keyword.iotinsurance_short}} 服務並部署必要支援服務及應用程式之後，即可建立授權使用者與防護的關聯來測試服務。
{:shortdesc}

**必要條件：**開始之前，請確定已具有下列必要條件：

- 電腦上所安裝的 [Node.js](https://nodejs.org/en/)。  
- 已啟用 Node.js 的運行環境（例如 Eclipse）。
- Git 軟體及 [API 範例的 GitHub 原始碼儲存庫](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)的存取。或者，您可以下載[保存與原始碼檔案](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)。
- 備妥的原始碼。
  若要準備原始碼，請執行下列動作：
  1. 將 [GitHub 原始碼儲存庫](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)複製或下載至電腦。
  2. 使用命令提示字元以移至包含所複製原始碼檔案的資料夾，並執行 `npm install` 指令，來安裝專案的開放程式碼必要條件。

建立可用來測試儀表板特性及範例行動應用程式的使用者。

1. 在 {{site.data.keyword.iotinsurance_short}} 系統中，建立使用者。
  1. 編輯 createUser.js 檔案，以將 **user** 變數中的值取代為唯一使用者資訊。
  2. 儲存檔案。
  3. 執行 `node createUser.js`。此處理程序需要幾分鐘才能完成。
  4. 記下使用者名稱；它是下一步中的必要項目。
2. 建立使用者的防護關聯。
  1. 編輯 createUserShieldAssociation.js 檔案，以在 **username** 變數中新增前一個步驟中的使用者名稱。
  2. 儲存檔案。
  3. 執行 `node createUserShieldAssociation.js`。如需防護的相關資訊，請參閱[元件](iotinsurance_overview.html#components})。
3. （選用）自動更新分析引擎；不過，如果未顯示正確的資料，您可以執行 `node updateAnalyticsEngine.js` 來重新整理分析引擎。
4. （選用）模擬使用者的危害事件。
  1. 編輯 simulateHazard.js 檔案，以在 **usr** 變數中新增先前步驟中的使用者名稱。
  2. 儲存檔案。
  3. 執行 `node simulateHazard.js`。
5. （選用）執行 `node createHistoricalData.js`，以建立一組模擬歷程資料。


# 相關鏈結
{: #rellinks}

## API 參考資料
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API 範例](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 相關鏈結
{: #general}
* [開發人員支援討論區](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack Overflow 支援討論區](http://stackoverflow.com/questions/tagged/ibm-bluemix)
