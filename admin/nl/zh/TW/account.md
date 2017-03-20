---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 管理 {{site.data.keyword.Bluemix_notm}} 帳戶
{: #mngacct}

移至**帳戶**鏈結，以設定通知、檢視帳戶用量，或檢視帳單。
{:shortdesc}

## 註冊 {{site.data.keyword.Bluemix_notm}}
{: #signup}

您可以使用現有 IBM ID 來註冊 {{site.data.keyword.Bluemix_notm}} 帳戶，方法是建立新的 IBM ID 或使用聯合 ID。聯合 ID 是公司網域內已向 IBM 註冊的 ID，因此您可以使用網域及使用者認證來存取 IBM Web 應用程式。  

只有在公司已與 IBM 合作登錄時，才能使用聯合 ID 來註冊 {{site.data.keyword.Bluemix_notm}}。向 IBM 登錄公司網域，可讓使用者使用其現有公司使用者認證來登入 IBM 產品和服務。然後，透過公司的身分提供者來處理鑑別。當您使用聯合 ID 登入 {{site.data.keyword.Bluemix_notm}} 時，系統會提示您透過公司的登入頁面進行登入。如需要求向 IBM 登錄公司或組織網域的相關資訊，或處理程序的相關資訊，請參閱 [IBMid Enterprise Federation Adoption Guide ![外部鏈結圖示](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}。當您要求登錄聯合 ID 時，需要有 IBM 贊助者（例如供應項目代言人或用戶端代言人）。

| 註冊方法 | 詳細資料 |    
|-----------------|---------|
|現有 IBM ID | 如果您已經有 IBM ID，請使用用於其他 IBM 產品及服務的現有認證來註冊 {{site.data.keyword.Bluemix_notm}}。您需要在註冊時輸入電話號碼。 |
|新的 IBM ID | 如果您還沒有 IBM ID，則可以選擇建立 IBM ID。IBM ID 可讓您將一個登入使用者名稱用於所有使用的 IBM 產品及服務（包括 {{site.data.keyword.Bluemix_notm}}）。您需要輸入個人資訊，包括新認證的名字和姓氏、電話號碼及密碼。使用其他 IBM 產品及服務時，您可以使用此 IBM ID 進行登入。  |
|聯合 ID | 如果您的公司要求向 IBM 登錄公司網域中的使用者認證，您可以使用已用於公司登入的認證來註冊 {{site.data.keyword.Bluemix_notm}}。您需要在註冊時輸入電話號碼。 |
{: caption="表 1. 註冊方法" caption-side="top"}

## 設定通知
{: #notifications}

按一下**帳戶** &gt; **通知**，以設定一般帳戶及消費通知。消費通知僅適用於「訂閱」和「隨收隨付制」的 {{site.data.keyword.Bluemix_notm}} 帳戶擁有者。

您可以針對 {{site.data.keyword.Bluemix_notm}} 突發事件和計劃性的維護作業設定平台電子郵件通知，並可設定消費通知，以在帳戶接近您指定的消費臨界值時警示您。請完成下列作業，為您的帳戶設定不同的通知類型。

### 設定平台通知

按一下**帳戶** &gt; **通知** &gt; **平台**，以針對 {{site.data.keyword.Bluemix_notm}} 突發事件及計劃性維護作業來設定電子郵件通知。您可以選取或清除每一個選項，以啟用或停用電子郵件通知。

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### 設定消費通知
{: #spendingnotifications}

如果您是「訂閱」或「隨收隨付制」的 {{site.data.keyword.Bluemix_notm}} 帳戶擁有者，即可設定電子郵件消費通知。設定對於下列項目的通知：總帳戶消費、總運行環境消費、總容器消費及總服務消費，以及個別服務的消費（協力廠商服務除外）。您會在達到所指定消費臨界值的 80%、90% 和 100% 時收到通知。您可以在需求變更時隨時編輯每一個消費通知。

完成下列步驟，以設定消費限制的電子郵件通知：

<ol>
<li>按一下**帳戶** &gt; **通知** &gt; **消費**。</li>
<li>輸入數值，以針對每一種通知類型來設定觸發通知的消費臨界值：<br />
<ul>
<li>帳戶總計</li>
<li>運行環境總計</li>
<li>服務總計</li>
<li>容器總計</li>
<li>特定服務的消費</li>
</ul>
</li>
<li>完成時，請按一下**儲存**。</li>
</ol>

**附註**：如果您有試用帳戶，則可以升級至「訂閱」或「隨收隨付制」帳戶來設定消費限制。如需「隨收隨付制」及「訂閱」帳戶的相關資訊，請參閱[計費方式](/docs/pricing/index.html#pay-accounts)。

## 檢視用量
{: #acctusage}

身為組織的帳戶擁有者或帳單管理員，您可以使用「用量儀表板」頁面，來查看組織中每個月所使用的運行環境、容器、服務及支援的即時費用。您可以查看所有地區的運行環境 GB-小時和服務耗用量，或選擇查看特定地區。

若要開啟「用量儀表板」頁面，請按一下**帳戶** &gt; *your_account_name* &gt; **用量儀表板**。帳單管理員只能針對他們身為帳單管理員的組織看到其詳細資料。

在每一個計費週期的結尾，會針對跨所有組織發生的用量總計，向帳戶擁有者收費。身為帳戶擁有者，您可以依地區和組織來過濾用量摘要。您也可以按一下特定月份，以查看該月份的用量。從**組織**清單中選取**所有組織**，以查看帳戶中所有組織的用量。

## 更新計費資訊
{: #account_billing}

身為帳戶擁有者，您可以編輯、新增或移除與 {{site.data.keyword.Bluemix_notm}} 帳戶相關聯的預存信用卡資訊。按一下**帳戶** &gt; *your_account_name* &gt; **計費**。

如果您有 SoftLayer 帳戶鏈結至 {{site.data.keyword.Bluemix_notm}} 帳戶，請參閱[帳戶鏈結後的 {{site.data.keyword.Bluemix_notm}} 用量計費](/docs/admin/softlayerlink.html#bill_usage)，以取得計費方式的相關資訊。
