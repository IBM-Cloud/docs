---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 定義原則
{: #criteria}

使用 {{site.data.keyword.DRA_short}}，定義您應用程式的原則十分簡單。若要開始進行，請遵循下列步驟：
{:shortdesc}

1. 在側邊功能表上，按一下**原則**。

2. 按一下**建立原則 (+)**，然後輸入新原則的名稱及說明。

3. 按**下一步**。

4. 至少將一個規則新增至原則：
  1. 按一下**建立規則 (+)**。
  2. 選取規則類型。
  3. 輸入規則的詳細資料及條件。
  4. 按一下**儲存**。

5. 完成將規則新增至原則時，請按一下**完成**。

原則是在已新增 {{site.data.keyword.DRA_short}} 的 {{site.data.keyword.Bluemix_notm}} 組織中建立的。相同組織中的任何應用程式都可以使用此原則。

{{site.data.keyword.DRA_short}} 支援下列類型的度量值及格式：

* 功能驗證測試（Mocha、JUnit）
* 單元測試（Mocha、JUnit、Karma/Mocha）
* 程式碼涵蓋面（Istanbul 作為 JSON 摘要報告格式、Blanket.js）

{{site.data.keyword.DRA_short}} 也支援 Selenium 及 Jasmine 測試。這些測試必須內含在正式支援的工具（例如 JUnit、xUnit 及 Mocha）中。若要進一步瞭解如何一起使用 {{site.data.keyword.deliverypipeline}}、{{site.data.keyword.DRA_short}} 及 Selenium，請參閱[從指令行在交付管線上執行 Selenium 測試](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/)。

針對具有測試案例的項目，您可以指定重要測試案例，這些測試案例就是不論可接受百分比為何都必須通過的測試。重要測試案例名稱必須符合測試案例的 `full title` 屬性：    
* 針對 Karma/Mocha 測試，使用空格將 `describe()` 與 `it()` 說明字串鏈結在一起
* 針對 JUnit 測試，使用空格將套件名稱、類別名稱與函數名稱鏈結在一起    

您可以將 Sauce Labs 整合新增至管線，以搭配使用 Sauce Labs 與 {{site.data.keyword.DRA_short}}。然後，將 `SAUCE_USERNAME` 及 `SAUCE_ACCESS_KEY` 環境變數併入 Selenium 測試中，以當作認證。

在執行之後，您可以看到日誌中所有測試的完整標題。  

附註：
* {{site.data.keyword.DRA_short}} 不支援完整標題中包含連字號的重要測試。    
* 如果您變更您的組織名稱，則必須重建與前一個名稱相關聯的原則。您將會中斷與已在名稱變更之前產生的決策報告的存取。

## 建立功能驗證測試規則
{: #criteria_fvt}

1. 鍵入說明，並選取格式。

2. 指定必須通過才能宣告成功的測試案例的百分比。

3. 定義任何重要測試案例。

4. 若要監視測試案例回歸，請選取**監視測試案例回歸**勾選框。

5. 按一下**儲存**。


## 建立單元測試規則
{: #criteria_ut}

1. 鍵入說明，並選取格式。

2. 指定必須通過才能宣告成功的測試案例的百分比。

3. 定義任何重要測試案例。

4. 若要監視測試案例回歸，請選取**監視測試案例回歸**勾選框。

5. 按一下**儲存**。


## 建立程式碼涵蓋面規則
{: #criteria_codecoverage}

1. 鍵入說明，並選取格式。

2. 指定需要宣告成功的程式碼涵蓋面的百分比。

3. 若要監視程式碼涵蓋面回歸，請選取**監視測試案例回歸**勾選框。

4. 按一下**儲存**。
