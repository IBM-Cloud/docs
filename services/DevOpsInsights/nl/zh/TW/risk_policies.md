---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 建立原則和規則
{: #policies_and_rules}

原則是在交付管線中用來控制閘道的規則集。如果您的程式碼不符合或超出特定閘道制定的原則，則會中止部署，以防止釋出有風險的變更。

您可以在 {{site.data.keyword.DRA_short}} 中定義原則。原則會建立在包含 {{site.data.keyword.DRA_short}} 的 {{site.data.keyword.Bluemix_notm}} 組織 (org) 中。相同組織中的任何應用程式都可以使用此原則。 

## 建立原則
{: #create_policies}

若要建立原則，請執行下列動作：

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
{: #creating_rules}

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

您可以將 {{site.data.keyword.DRA_short}} 與 IBM Application Security on Cloud 整合，以執行 static-code 和 dynamic-app 掃描。如需 Application Security on Cloud 的相關資訊，請參閱[正式文件](/docs/services/ApplicationSecurityonCloud/index.html)。

1. 鍵入說明。

2. 指定規則可容許的高嚴重性、中嚴重性和低嚴重性問題數上限。 

3. 按一下**儲存**。

### 建立動態安全掃描規則
{: #criteria_dynamic}

您可以將 {{site.data.keyword.DRA_short}} 與 {{site.data.keyword.appseccloudfull}} 整合，以執行 dynamic-app 掃描。如需 Application Security on Cloud 的相關資訊，請參閱[正式文件](/docs/services/ApplicationSecurityonCloud/index.html)。

1. 鍵入說明。

2. 指定規則可容許的高嚴重性、中嚴重性和低嚴重性問題數上限。 

3. 按一下**儲存**。
