---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 定義原則
{: #policies}

原則可控制持續交付管線中的閘道。如果您的程式碼不符合或超出特定閘道制定的原則，則會中止部署，以防止釋出有風險的變更。
{:shortdesc}

您可以在 {{site.data.keyword.DRA_short}} 中定義原則。原則會建立在包含 {{site.data.keyword.DRA_short}} 的 {{site.data.keyword.Bluemix_notm}} 組織 (org) 中。相同組織中的任何應用程式都可以使用此原則。 

若要定義原則，請執行下列動作：

1. 從左導覽中，按一下**設定**。

2. 按一下**原則**。

3. 按一下**建立原則**，然後鍵入新原則的名稱和說明。

4. 按**下一步**。

4. 至少將一個規則新增至原則：
  1. 按一下**新增規則至原則**。
  2. 選取規則類型。
  3. 輸入規則的詳細資料及條件。
  4. 按一下**儲存**。

5. 完成將規則新增至原則時，請按一下**完成**。

## 建立規則
{: #criteria}

規則可定義原則用來判斷成功或失敗的準則。您可以建立「單元測試和測試涵蓋面」原則，其中包含的單元測試規則需要 80% 單元測試成功，而測試涵蓋面規則需要 100% 程式碼涵蓋面。如果您新增的閘道在管線中參照此規則，該閘道會阻擋未同時滿足這兩項規則的任何建置繼續進行。 

如果無論如何都必須成功，您可以將測試標示為重要。若要建立規則，請選取原則，然後按一下**新增規則至原則**。 

### 建立功能驗證測試規則
{: #criteria_fvt}

1. 鍵入說明，並選取格式。

2. 指定必須通過才能宣告成功的測試案例的百分比。

3. 定義任何重要測試案例。

4. 若要監視測試案例回歸，請選取**監視測試案例回歸**勾選框。

5. 按一下**儲存**。


### 建立單元測試規則
{: #criteria_ut}

1. 鍵入說明，並選取格式。

2. 指定必須通過才能宣告成功的測試案例的百分比。

3. 定義任何重要測試案例。

4. 若要監視測試案例回歸，請選取**監視測試案例回歸**勾選框。

5. 按一下**儲存**。


### 建立程式碼涵蓋面規則
{: #criteria_codecoverage}

1. 鍵入說明，並選取格式。

2. 指定需要宣告成功的程式碼涵蓋面的百分比。

3. 若要監視程式碼涵蓋面回歸，請選取**監視測試案例回歸**勾選框。

4. 按一下**儲存**。

### 建立靜態安全掃描規則
{: #criteria_static}

1. 鍵入說明。

2. 指定規則可容許的高嚴重性、中嚴重性和低嚴重性問題數上限。 

3. 按一下**儲存**。

### 建立動態安全掃描規則
{: #criteria_dynamic}

1. 鍵入說明。

2. 指定規則可容許的高嚴重性、中嚴重性和低嚴重性問題數上限。 

3. 按一下**儲存**。

## 測試結果格式和工具

{{site.data.keyword.DRA_short}} 支援下列類型的度量值及格式：

* 功能驗證測試（Mocha、xUnit）
* 單元測試（Mocha、xUnit、Karma/Mocha）
* 程式碼涵蓋面（Istanbul 作為 JSON 摘要報告格式、Blanket.js）

{{site.data.keyword.DRA_short}} 也支援 Selenium 及 Jasmine 測試。這些測試必須內含在正式支援的工具中，例如 JUnit 和 Mocha。若要進一步瞭解如何一起使用 {{site.data.keyword.deliverypipeline}}、{{site.data.keyword.DRA_short}} 及 Selenium，請參閱[從指令行在交付管線上執行 Selenium 測試](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/)。

針對具有測試案例的項目，您可以指定重要測試案例，這些測試案例就是不論可接受百分比為何都必須通過的測試。重要測試案例名稱必須符合測試案例的 `full title` 屬性。    
* 若為 Karma/Mocha 測試，會使用空格將 `describe()` 與 `it()` 說明字串鏈結在一起。
* 若為 xUnit 測試，會使用空格將套件名稱、類別名稱與函數名稱鏈結在一起。舉例說明如下：
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  該範例會產生下列測試案例名稱：
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

您可以將 Sauce Labs 工具整合新增至管線，以搭配使用 Sauce Labs 與 {{site.data.keyword.DRA_short}}。然後，將 `SAUCE_USERNAME` 及 `SAUCE_ACCESS_KEY` 環境變數併入 Selenium 測試中，以當作認證。

執行之後，您可以在日誌中看到所有測試的完整標題。  

**附註：**
* {{site.data.keyword.DRA_short}} 不支援完整標題中包含連字號的重要測試。    
* 如果您變更您的組織名稱，則必須重建與前一個名稱相關聯的原則。您將無法存取名稱變更之前產生的任何決策報告。

## 檢視決策報告    
{: #DI_decision_reports}

管線執行之後，{{site.data.keyword.DRA_short}} 會開始收集並分析其測試結果，以建立基準線。收集每個後續執行的資料，並將其與先前的結果進行比較。決策閘道使用此資料來判斷何時停止部署。 

若要從管線檢視閘道的決策報告，請完成下列步驟：

   1. 在包含要檢查之閘道的階段上，按一下 **View logs and history**。

   2. 從包含閘道的工作中，按一下閘道的名稱。

   3. 在日誌視圖中，尋找 `Check {{site.data.keyword.DRA_short}} report here` 訊息，然後按一下鏈結來開啟報告。
